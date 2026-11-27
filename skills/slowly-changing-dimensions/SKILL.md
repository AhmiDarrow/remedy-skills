---
name: slowly-changing-dimensions
version: 1.0.0
description: >
  Track history in dimension tables with the right change type, validity ranges and point-in-time joins. Use when reports must show attributes as they were at the time of each event.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - modeling
  - warehouse
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: slowly-changing-dimensions
  official: true
  domain: data
  security_flags: []
---

# Slowly Changing Dimensions

## When to use
Attributes such as region, plan or owner change, and old facts must keep or intentionally lose their original grouping.

## Steps
1. For each attribute ask whether reports need the value at event time, the current value, or both.
2. Overwrite (type 1) for corrections and attributes where history does not matter; add a version row (type 2) where it does.
3. For type 2, include a surrogate key, the business key, `valid_from`, `valid_to`, a current flag and a hash of tracked columns.
4. Use half-open ranges: `event_time >= valid_from AND event_time < valid_to`. Use one convention for open ends, either NULL or a far-future date.
5. On load, compare tracked values with a null-safe comparison. Close the current row and insert the new one in one transaction.
6. Take `valid_from` from the source's change time when reliable; if only snapshot time exists, document that precision.
7. Decide how to treat a late-arriving change (split the existing range) and a delete (close the range).
8. Resolve the surrogate key onto facts at load time, with a placeholder member for dimensions not yet arrived, and a rule for repairing them.
9. Test that each business key has no overlaps, no unintended gaps and exactly one current row while active, and that rerunning a load adds nothing.

## Watch out for
- `BETWEEN` with inclusive ends matches two versions at the boundary and doubles facts.
- Tracking volatile columns such as last login creates a new version every load.
- History cannot be reconstructed from a source that only holds current state; say when tracking began.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Overlap and current-row tests pass, a second identical load changes nothing, and a point-in-time query returns the old attribute for an old event.
