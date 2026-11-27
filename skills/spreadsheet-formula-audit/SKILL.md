---
name: spreadsheet-formula-audit
version: 1.0.0
description: >
  Audit a workbook's formulas for silent errors before its numbers are trusted. Use for inherited spreadsheets, surprising totals, or a model about to inform a decision.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - spreadsheets
  - review
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: spreadsheet-formula-audit
  official: true
  domain: data
  security_flags: []
---

# Spreadsheet Formula Audit

## When to use
A workbook produces numbers and nobody has checked how.

## Steps
1. Work on a copy. List sheets including hidden and very hidden ones, named ranges, external links and macros. Do not run macros.
2. Dump formulas and values separately. With openpyxl, `load_workbook(path)` gives formulas and `data_only=True` gives the last cached results; it does not recalculate, and saving the data_only load destroys formulas.
3. Search cached values for `#REF!`, `#N/A`, `#DIV/0!`, `#VALUE!`, `#NAME?`.
4. Compare formulas down each column in relative form and flag breaks in the pattern, especially a typed number among formulas.
5. Check that SUM and lookup ranges include the last data row, and look for rows added below a range.
6. Check lookups for exact versus approximate matching. VLOOKUP without its fourth argument matches approximately.
7. Find hardcoded constants inside formulas, error-swallowing IFERROR wrappers, circular references and volatile functions.
8. Test key outputs independently by recomputing from raw rows, and change one input to see that expected cells move.
9. Report findings by cell address with effect on results; fix only with approval.

## Watch out for
- Numbers stored as text are skipped by SUM without any error.
- Hidden rows and filters change what the user thinks is totalled; SUM includes them.
- A matching grand total can hide two offsetting errors.
- Recalculating in a different application may give different results for newer functions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each finding has a cell address and impact, the key outputs are independently reproduced or flagged, and the original file is unchanged.
