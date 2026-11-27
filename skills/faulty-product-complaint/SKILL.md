---
name: faulty-product-complaint
version: 1.0.0
description: >
  Get a repair, replacement or refund for faulty or misdescribed goods or services with a clear written complaint. Use when a seller or provider is not putting a problem right.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - disputes
  - consumer
kind: native
status: discovered
tools:
  - read
  - write
  - web.search
  - web.fetch
  - mail.send
metadata:
  source: library
  library_id: faulty-product-complaint
  official: true
  domain: personal
  security_flags: []
---

# Faulty Product Complaint

## When to use
Something bought is broken, not as described or badly done.

## Steps
1. Collect proof of purchase, the listing or contract, photos, dates (bought, delivered, fault noticed, reported) and every reply so far.
2. Find the consumer rights for the buyer's location on an official or established consumer advice site. Distinguish a change-of-mind return policy from statutory rights for faults. Private sales often carry fewer rights. Cite page and date; do not declare who will win.
3. Identify who owes the remedy; it is often the seller, even if the maker offers its own warranty.
4. Choose one specific remedy and an acceptable fallback.
5. Draft: order reference, short dated facts, what is wrong, the term or right relied on, remedy sought, reply date, attachments. One page, no insults.
6. Show the draft; send with `mail.send` only after approval, or let the person use the seller's form and save a copy.
7. On the deadline, escalate in order: formal complaint, ombudsman or dispute scheme if one covers the trader, card or payment provider, small claims. Check time limits for each early.

## Watch out for
- Repairing it yourself or discarding it before the seller can inspect.
- Return postage without tracking.
- Accepting store credit by default when another remedy was sought.
- Letting the card dispute window lapse while waiting for replies.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A dated written complaint with a named remedy is on record, and the next escalation and its time limit are known.
