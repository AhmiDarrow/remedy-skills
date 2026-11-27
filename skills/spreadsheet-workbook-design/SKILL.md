---
name: spreadsheet-workbook-design
version: 1.0.0
description: >
  Design a new workbook that stays correct as people keep adding data. Use when building a tracker, calculator or simple model from scratch.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - spreadsheets
  - design
kind: native
status: discovered
tools:
  - write
  - bash
  - read
metadata:
  source: library
  library_id: spreadsheet-workbook-design
  official: true
  domain: data
  security_flags: []
---

# Spreadsheet Workbook Design

## When to use
The user needs a spreadsheet they will fill in and maintain.

## Steps
1. List the questions it must answer and who will enter data. Derive columns from those.
2. Separate sheets by role: inputs and assumptions, raw records, calculations, summary.
3. Make the records sheet one row per event or item, one fact per column, one header row, no merged cells or blank spacer rows. Never spread months across columns for data entry.
4. Give each record a stable ID.
5. Use a structured table or clearly bounded ranges so new rows are included in formulas.
6. Put every rate or threshold in a labelled cell with its unit and reference it.
7. Add data validation: dropdowns from a list sheet, date and number limits.
8. Add check cells, such as summary total equals records total, that show a visible pass or fail.
9. Test with a few made-up rows including a blank, a negative, a duplicate and a row appended at the end, then clear test data.

## Watch out for
- Colour as the only way to record status cannot be filtered reliably or calculated.
- Whole-sheet copies per month make cross-period questions painful; use a date column.
- Files written by a library contain formulas without computed values until an application calculates them, so open or recalculate before claiming results.
- Sheet protection prevents accidents but is not security.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
An appended test row flows into the summary, check cells pass, and invalid entries are rejected or flagged.
