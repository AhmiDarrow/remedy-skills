---
name: welcome-email-sequence
version: 1.0.0
description: >
  Draft an onboarding email sequence for people who opted in, with one goal per message and exit rules. Use when new subscribers or trial users get no useful follow-up.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - marketing
  - email
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: welcome-email-sequence
  official: true
  domain: content
  security_flags: []
---

# Welcome Email Sequence

## When to use
Someone signs up and the sender wants to help them reach first value. Drafts only; the user loads and activates them.

## Steps
1. Define the entry event, what the person agreed to receive, and the single behaviour the sequence should produce.
2. Find the steps between signup and first value, and the points where people stall, from data or support questions.
3. Plan three to six messages, one action each. The first delivers what signup promised.
4. Write triggers around behaviour where the platform supports it: skip the setup nudge for people already set up.
5. Set exits: goal reached, purchase, unsubscribe, bounce, or an open support complaint.
6. For each message give subject, preview text, body and one primary link, with a fallback for every merge field.
7. Include sender identity, postal address where required and a working unsubscribe. Have consent rules for the recipients' regions checked by someone qualified.
8. Specify the metric per message and test sends to the user's own addresses.

## Watch out for
- Adding purchased or scraped addresses; refuse this.
- Judging success by opens, which privacy features inflate.
- "Hi ," from an empty name field.
- Overlap with other campaigns sending the same day.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each message has one action, trigger, exit rules and merge fallbacks, and nothing has been activated without the user.
