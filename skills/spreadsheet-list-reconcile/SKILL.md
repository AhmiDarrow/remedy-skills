---
name: spreadsheet-list-reconcile
version: 1.0.0
description: >
  Compare two lists or ledgers and explain every unmatched or differing row. Use when two exports should agree, such as registrations against payments or inventory against a count.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - spreadsheets
  - reconciliation
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: spreadsheet-list-reconcile
  official: true
  domain: data
  security_flags: []
---

# Spreadsheet List Reconcile

## When to use
Two datasets describe the same things and the totals or members differ.

## Steps
1. Record each source's origin, export time, filters, row count and control total.
2. Choose the match key. Prefer a shared unique ID; otherwise a composite such as date, amount and reference.
3. Check key uniqueness within each list first. Duplicates cause multiplied joins and must be reported or aggregated.
4. Normalise keys into new columns: trim, case, non-breaking spaces, leading zeros, date formats, sign conventions.
5. Do an outer join (pandas `merge(how="outer", indicator=True)` or lookups in both directions).
6. Split results into matched and equal, matched with differences, only in A, only in B, ambiguous.
7. Compare money as integer cents or decimals with a stated tolerance, not raw floating point equality.
8. Run looser second passes (date window, fuzzy name) only as suggestions marked for human confirmation.
9. Show a bridge from total A to total B made of those categories, with the remaining unexplained amount.

## Watch out for
- A one-direction lookup never finds records missing from the first list.
- Exports taken at different times produce timing differences, not errors.
- Auto-accepting fuzzy matches can pair two different people.
- Do not edit either source to force agreement.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every row from both lists is in exactly one category and the bridge reaches the second total or states the unexplained remainder.
