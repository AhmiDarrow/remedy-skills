---
name: ics-file-handling
version: 1.0.0
description: >
  Inspect, fix or create .ics calendar files so events import with the right times and no duplicates. Use when an invite file shows wrong hours or a schedule must be bulk added.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - calendar
  - files
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
  - calendar.list_events
metadata:
  source: library
  library_id: ics-file-handling
  official: true
  domain: tooling
  security_flags: []
---

# Ics File Handling

## When to use
Events are arriving or leaving as an iCalendar file.

## Steps
1. Open the file as text and count `BEGIN:VEVENT` blocks. Review summaries, links and attendees before anyone imports it, especially from unknown senders.
2. Classify each start: UTC (ends in `Z`), zoned (`DTSTART;TZID=...`), floating (neither, so it follows the viewer's zone) or all-day (`VALUE=DATE`).
3. For all-day events, remember that DTEND is exclusive: a one-day event on the 5th ends on the 6th.
4. Check `RRULE`, `EXDATE` and `RECURRENCE-ID` overrides together, and list expanded dates for the first few months.
5. When creating, give every event a unique stable `UID`, a `DTSTAMP`, start, end and summary, inside a `VCALENDAR` with `VERSION:2.0` and `PRODID`.
6. Escape commas, semicolons, backslashes and newlines in text values, use CRLF line endings and fold long lines. A maintained iCalendar library handles this better than string joining.
7. Import into a new empty test calendar first and compare listed events with the source schedule.
8. Import into the real calendar only after approval.

## Watch out for
- Reimporting with new UIDs creates duplicates; keeping the UID lets many clients treat it as an update, though behaviour varies.
- A TZID with no matching definition or an unrecognised name may be shown as floating time.
- `METHOD:REQUEST` or attendee lines can make some clients treat it as an invitation and send responses.
- Removing events one at a time after a bad import is tedious, which is why the test calendar matters.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Event count, local times and recurrence dates in the test calendar match the intended schedule.
