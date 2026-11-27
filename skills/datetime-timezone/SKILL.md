---
name: datetime-timezone
version: 1.0.1
description: >
  Fix date and time bugs by deciding whether each value is an instant, a local wall time or a plain date, then testing clock changes. Use when times shift by hours, dates move by a day or schedules drift.
author: Remedy Official
license: Apache-2.0
tags:
  - quality
  - backend
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: datetime-timezone
  official: true
  security_flags: []
---

# Datetime Timezone

## When to use
Displayed or stored times are wrong for some users, or code schedules across time zones.

## Steps
1. Reproduce with an exact input, the zone of browser, server, database session and job runner, and expected versus actual output. A whole-hour offset or a one-day shift tells you where to look.
2. Trace the value through parsing, type, storage, serialization and display, printing its offset at each hop.
3. Classify each field. Instant (something happened): store UTC or an offset-aware type. Plain date (birthday, due date): store a date with no time or zone conversion. Future local event ("09:00 in Lisbon"): store wall time plus the IANA zone name, since zone rules can change.
4. Check library traps: in JavaScript a date-only string parses as UTC but a date-time without offset parses as local; in Python avoid naive values and `utcnow()` and use `zoneinfo`; in PostgreSQL `timestamptz` keeps the instant, not the original zone.
5. Send instants over APIs in RFC 3339 with `Z` or an offset. Never use abbreviations such as "CST".
6. Define local times that do not exist or occur twice at clock changes, and pick the behaviour explicitly.
7. Distinguish "add 24 hours" from "same time tomorrow". Query day ranges as start inclusive, next start exclusive, computed in the intended zone.
8. Inject the clock and add tests for a spring and autumn change, a non-hour offset zone, a month end and 29 February.
9. If stored data is wrong, identify the affected rows by when and how they were written before proposing a correction.

## Watch out for
- Shifting all old rows by a fixed offset breaks those written under the other daylight rule.
- A server set to UTC hides bugs that appear on developer machines, and the reverse.
- A fixed offset like `+01:00` is not a time zone.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The reproduction now gives the expected value with the process run in at least two different zones, and the clock-change tests pass.
