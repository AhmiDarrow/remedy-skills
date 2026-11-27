---
name: star-schema-modeling
version: 1.0.0
description: >
  Model analytics data as fact and dimension tables with a declared grain, additive measures and shared dimensions. Use when building a reporting layer or warehouse mart from operational tables.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - modeling
  - warehouse
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: star-schema-modeling
  official: true
  domain: data
  security_flags: []
---

# Star Schema Modeling

## When to use
Analysts rebuild the same complicated joins, and different reports disagree.

## Steps
1. Choose one business process (orders, payments, support tickets) and gather the real questions asked of it.
2. Declare the grain in a sentence, such as one row per order line. Prefer the most detailed level available.
3. List dimensions that are single-valued at that grain: date, customer, product, channel.
4. List measures true at that grain. Mark each additive, semi-additive (balances add across accounts, not across time) or non-additive (ratios).
5. Store numerators and denominators so ratios are computed after aggregation.
6. Never mix grains in one fact. An order-level shipping fee needs a documented allocation or its own fact.
7. Choose the fact style: transaction, periodic snapshot or accumulating snapshot.
8. Build conformed dimensions shared across facts, with the same keys and definitions, plus explicit unknown members instead of NULL foreign keys.
9. Handle many-to-many with a bridge table and a stated weighting rule.
10. Role-play the date dimension for order, ship and refund dates and name which one each metric uses.
11. Test grain uniqueness, key coverage and reconciliation to the source.

## Watch out for
- Joining two fact tables directly fans out rows; aggregate each to shared dimensions, then combine.
- Dimensions split into many normalized subtables push complexity back onto every query.
- Local timestamps converted to dates without a stated business time zone move sales between days.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Grain is documented and tested, the gathered questions are answered with straightforward queries, and totals reconcile with the source.
