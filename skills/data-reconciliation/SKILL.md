---
name: data-reconciliation
version: 1.0.0
description: >
  Explain why two systems or reports disagree by aligning definitions and drilling from totals down to individual records. Use when figures that should match do not.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - quality
  - debugging
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: data-reconciliation
  official: true
  domain: data
  security_flags: []
---

# Data Reconciliation

## When to use
A dashboard differs from the source system, finance export or an older pipeline.

## Steps
1. Record both numbers exactly, with the query or report, filters, and when each was pulled.
2. Compare definitions before data: what is counted, which timestamp assigns the period, time zone, currency and conversion date, gross or net, refunds, cancellations, test accounts, rounding point.
3. Check freshness. A moving source needs both sides cut at the same instant, or a period closed long enough to be stable.
4. Narrow by splitting the totals by day, then by a category, and follow only the slices that differ.
5. In a differing slice, full outer join on the business key and classify rows: only in A, only in B, both with different values.
6. Check duplicate keys on each side before joining.
7. Compare values with null-safe logic and exact decimals, applying a tolerance only where a known rounding rule justifies it.
8. Quantify each cause and build a bridge from A to B: starting figure, each adjustment with amount and count, ending figure, unexplained remainder.
9. State which definition each side implements and let the owner decide which is correct before changing anything.
10. Turn the reconciliation into a repeatable query with an alert on the unexplained remainder.

## Watch out for
- Matching totals can hide offsetting errors; compare keys as well.
- Adjusting filters until the numbers agree, without a reason for each, fits noise.
- Soft deletes, later edits and backdated entries make last month's figure legitimately change between pulls.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The bridge accounts for the difference down to a stated remainder, with sample records for every cause.
