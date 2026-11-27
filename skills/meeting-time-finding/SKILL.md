---
name: meeting-time-finding
version: 1.0.0
description: >
  Propose meeting slots from calendar data, across time zones and clock changes, and create the event after approval. Use when asked to find a time or book a meeting with others.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - calendar
  - meetings
kind: native
status: discovered
tools:
  - calendar.list_events
  - calendar.create_event
  - memory.search
  - bash
metadata:
  source: library
  library_id: meeting-time-finding
  official: true
  domain: personal
  security_flags: []
---

# Meeting Time Finding

## When to use
A meeting needs a time that fits real constraints.

## Steps
1. Get purpose, required and optional attendees, duration, window, location or call method, and any deadline.
2. List events across the window, from every calendar the user connected.
3. Treat tentative, travel, out-of-office and all-day entries according to what they mean; ask when unclear.
4. Apply remembered preferences: working hours, protected blocks, meeting-free days. Add buffers for travel or back-to-back load.
5. State honestly whose availability you can see. For others, offer candidates to ask about rather than claiming they are free.
6. Offer three slots with trade-offs. Across zones, record each person's IANA zone (abbreviations are ambiguous), convert for the actual date with a time zone library rather than a remembered offset, and show every local weekday, date and time. For a series, fix an anchor zone and flag the weeks where regions change clocks on different dates.
7. If nothing fits, show what would unlock a slot: shorter duration, drop an optional attendee, move a named flexible event. Do not move it yourself.
8. After the user picks, re-list that period to catch new conflicts.
9. Show title, time with zone, attendees, location and description, and whether invitations will go out. Create after approval and read the event back.

## Watch out for
- Creating an event with guests may email them immediately.
- An empty slot on a calendar can still be lunch, school pickup or another time zone's night.
- Dates such as 04/05 are ambiguous; write the month name and weekday.
- Check that the weekday and date match.
- Give the stored event an explicit zone and read it back in another attendee's zone.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The user has verified slot options, or an approved event exists with the correct time, zone and attendees as read back.
