---
name: subscription-audit
version: 1.0.1
description: >
  Audit subscriptions from statements or a list, compare yearly cost with use and plan cancellations before renewals. Use when someone wants to cut recurring charges or find forgotten subscriptions.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - finance
kind: native
status: discovered
tools:
  - read
  - write
  - calendar.create_event
metadata:
  source: library
  library_id: subscription-audit
  official: true
  domain: personal
  security_flags: []
---

# Subscription Audit

## When to use
Recurring charges need to be found and decided on, using only material the user provides.

## Steps
1. Ask for a list or exported statements covering twelve months or more, so annual renewals appear. Also suggest checking phone app-store subscriptions, payment services, phone and internet bills and work or family-paid duplicates.
2. Record per item: service, billing name, amount, currency, cycle, next renewal, payment route, account holder and who uses it.
3. Normalise to yearly cost: weekly times 52, four-weekly times 13, monthly times 12, quarterly times 4. Flag price rises and ended trials.
4. Ask when each was last used and what breaks without it. A missing record is not proof of no use.
5. Note overlaps and cheaper tiers. Mark each keep, cancel, downgrade or ask; the user decides.
6. Before cancelling, check minimum term, notice period, early exit fee, when access ends, and what is lost: files, photos, email address, purchases, grandfathered price, shared users.
7. Export needed data first. Cancel through the provider or the store that bills it, and save the confirmation. The user performs the cancellation.
8. Add reminders ahead of renewal and notice deadlines, and check the next statement for further charges.

## Watch out for
- Deleting an app or blocking a card usually does not end the contract.
- Unrecognised charges may be fraud or a trading name; search the name, then contact the bank promptly.
- Counting savings before confirmation arrives.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every recurring charge in the material has a yearly cost and decision, and each cancellation has a deadline and a confirmation or pending status.
