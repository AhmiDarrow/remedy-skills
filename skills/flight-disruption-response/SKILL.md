---
name: flight-disruption-response
version: 1.0.0
description: >
  Handle a cancelled or badly delayed flight, securing a way onward first and a claim file second. Use when a flight is cancelled, delayed, overbooked or a connection is missed.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - travel
  - disruption
kind: native
status: discovered
tools:
  - read
  - write
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: flight-disruption-response
  official: true
  domain: personal
  security_flags: []
---

# Flight Disruption Response

## When to use
A trip is breaking down now, or has just done so.

## Steps
1. Get booking reference, ticket type (one ticket or separate ones), route, new status from the airline's own channel, and what the traveller must reach and by when.
2. Act on rebooking in parallel: airline app, desk queue and phone. Search alternative flights, nearby airports and rail so the traveller can request a specific option.
3. Before accepting a refund or voucher, explain that it may end the airline's duty to carry them. Check the terms.
4. Warn that skipping one flight segment can cancel the rest of a ticket; get changes confirmed by the airline.
5. Notify hotel, car hire and tour operators about late arrival so bookings are not cancelled as no-shows.
6. Collect evidence: boarding passes, notices with times, the stated reason, receipts for meals, transport and lodging.
7. Find which passenger-rights rules apply from the regulator's official page, since they depend on departure point, arrival and airline. Check care, rerouting and compensation separately.
8. Check travel insurance and card cover, and their notification deadlines. Draft claims for the traveller to submit.

## Watch out for
- On separate tickets the second airline may owe nothing for a missed connection.
- Fake support accounts replying to public complaints and asking for booking codes.
- Promising compensation before the cause and rules are known.
- The traveller pays and confirms any new booking.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The traveller has a confirmed onward plan or refund choice, dependent bookings are informed, and receipts are filed with claim deadlines.
