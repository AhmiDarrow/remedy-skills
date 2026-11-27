---
name: spreadsheet-pivot-summary
version: 1.0.0
description: >
  Summarise row-level data with pivots or grouped formulas and reconcile the result to the source. Use for questions like totals by month, category, owner or region.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - spreadsheets
  - analysis
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: spreadsheet-pivot-summary
  official: true
  domain: data
  security_flags: []
---

# Spreadsheet Pivot Summary

## When to use
There are many detail rows and the user wants grouped totals, counts or averages.

## Steps
1. State the question as measure, grouping and filter: "sum of amount by category per quarter, excluding cancelled".
2. Confirm the grain: what one row represents. Find subtotal rows, repeated headers and duplicated IDs that would double count.
3. Normalise grouping values (trailing spaces, case, spelling variants) in a helper column, keeping the original.
4. Make sure dates are real dates before grouping, and say whether quarters are calendar or fiscal.
5. Build the pivot, or use SUMIFS, COUNTIFS or pandas `pivot_table` when a static reproducible output is better. Keep blank categories visible as "(blank)"; pandas drops missing keys by default.
6. Choose count, sum, distinct count or median deliberately.
7. Reconcile grand total and row count to the filtered source, and account for every excluded row.
8. Present with units, the filter, and the data's as-of date.

## Watch out for
- Averaging group averages is wrong when group sizes differ; compute from detail rows.
- A pivot does not update by itself when source data changes; refresh and check the source range includes new rows.
- Percent-of-total depends on the base chosen (row, column, grand); label it.
- A single mistyped year creates a phantom group that is easy to overlook.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The summary reconciles exactly to included source rows, exclusions are counted, and filters and definitions are written beside it.
