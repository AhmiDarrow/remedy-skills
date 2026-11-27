---
name: home-maintenance-calendar
version: 1.0.0
description: >
  Build a year-round upkeep schedule from the actual systems in a home. Use when someone moves in, keeps missing servicing, or asks what to maintain and when.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - home
  - maintenance
kind: native
status: discovered
tools:
  - read
  - write
  - calendar.list_events
  - calendar.create_event
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: home-maintenance-calendar
  official: true
  domain: personal
  security_flags: []
---

# Home Maintenance Calendar

## When to use
A household wants upkeep on a calendar instead of discovering it when something fails.

## Steps
1. Inventory what is really there: heating type, hot water source, cooling, smoke and CO alarms, gutters and roof, drains, septic or mains sewer, well or mains water, chimney, pumps, filtering appliances. Do not list systems the home lacks.
2. For each item, take the interval from its manual or installer label (ask for a photo of the label and the model number). Mark any interval you had to assume as "unconfirmed".
3. Separate jobs into DIY, licensed or certified trade, and landlord's responsibility. For a rental, read the lease before assigning anything to the tenant; gas, fixed wiring and structural work are usually not theirs.
4. Place jobs by season in the local climate: heating service before the cold months, gutters after leaf fall, outdoor water shut-off before first frost where pipes can freeze. Ask the hemisphere and climate; never assume.
5. Record legal or insurance-required checks separately with the document that proves each was done. Confirm the requirement on a local official source or the policy.
6. Check `calendar.list_events` for existing entries, then propose events with lead time: trades book out, so the reminder to book goes weeks before the due month. Create them only after approval.
7. Write a log file with one row per job: item, interval, last done, next due, who, cost, receipt location.

## Watch out for
- Scheduling from the calendar year when the interval runs from the last service date.
- Alarms have a replacement date as well as a test routine; read the date printed on the unit.
- Twenty reminders in one month get ignored. Spread flexible jobs out.
- Filter intervals change with pets, dust and heavy use, so note what shortened them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every installed system has an interval with its source or an "unconfirmed" mark, a next-due date and an owner, and approved reminders are on the calendar.
