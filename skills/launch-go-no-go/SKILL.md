---
name: launch-go-no-go
version: 1.0.0
description: >
  Run a go or no-go decision for a release using agreed criteria, named owners and recorded risks. Use when a launch date is near and readiness is unclear.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - product
  - release
kind: native
status: discovered
tools:
  - read
  - write
  - todo
metadata:
  source: library
  library_id: launch-go-no-go
  official: true
  domain: docs
  security_flags: []
---

# Launch Go No Go

## When to use
Several functions must confirm readiness and someone must make the call.

## Steps
1. Name one decision maker and the decision time, early enough to stop cleanly.
2. Agree criteria in advance across product quality, operations, support, legal or privacy review, communications and billing where relevant.
3. Make each criterion binary or thresholded with an evidence source and owner.
4. Separate blockers from accepted-risk candidates before results arrive.
5. Collect evidence, not verbal "should be fine": test run, dashboard, signed review.
6. For each unmet item state user impact, mitigation, owner, and what accepting it means.
7. Confirm rollback: who triggers it, the signal threshold, time needed, and what cannot be undone.
8. Record go, go with conditions, or no-go. Conditions need a deadline and a consequence.
9. Set the first post-launch check time and who watches.

## Watch out for
- Redefining a blocker as minor on launch morning.
- Treating silence from a reviewer as approval.
- A rollback never rehearsed or impossible after a data change.
- A no-go with no new decision date.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every criterion has status and evidence, accepted risks name who accepted them, and the decision and rollback trigger are recorded.
