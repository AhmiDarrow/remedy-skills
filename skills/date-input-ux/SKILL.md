---
name: date-input-ux
version: 1.0.0
description: >
  Design date and date-range inputs that accept typing, handle locales and time zones, and work by keyboard. Use when users enter birthdays, bookings, deadlines or report ranges.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - forms
  - ux
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: date-input-ux
  official: true
  domain: frontend
  security_flags: []
---

# Date Input Ux

## When to use
A date picker forces clicking through decades, saves the wrong day for some users, or cannot be operated without a mouse.

## Steps
1. Classify the value: calendar date with no time (birthday), exact instant (meeting), or local wall time in a named zone (recurring event). Each is stored differently.
2. Match control to task. Known dates such as birthdays: typed fields. Near-future booking: calendar plus typing. Reporting: presets such as last 7 days plus a custom range.
3. Evaluate native `input type="date"` first; its value is `YYYY-MM-DD` while display follows the browser locale.
4. If building a calendar, use an accessible component that already exists, supporting arrow keys, Page Up and Page Down for months, Home and End, Escape, and announced month changes.
5. State the expected format beside typed fields, accept common separators, and echo the parsed date in words to remove day-month ambiguity.
6. Define range rules: inclusive or exclusive end, maximum length, same-day, and behaviour when the new start is after the end.
7. Disable unavailable days and also explain why in text; validate again on the server.
8. Take week start and month names from locale APIs.
9. Test in zones both ahead of and behind UTC, across a daylight saving change, month ends and 29 February.

## Watch out for
- `new Date('2027-03-01')` is parsed as UTC midnight and displays as the previous day west of UTC.
- Formatting a calendar date with `toISOString` after local construction can shift it a day.
- Min and max limits computed once at page load go stale in a tab left open overnight.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A chosen date round-trips unchanged under two opposite time zones, the whole interaction works by keyboard, and invalid or ambiguous input gets a specific message.
