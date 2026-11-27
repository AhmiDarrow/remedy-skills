---
name: spreadsheet-import-type-safety
version: 1.0.0
description: >
  Open or import delimited data without silently corrupting IDs, dates and long numbers. Use when a CSV loses leading zeros, shows scientific notation or swaps day and month.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - spreadsheets
  - import
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: spreadsheet-import-type-safety
  official: true
  domain: data
  security_flags: []
---

# Spreadsheet Import Type Safety

## When to use
Data must move into a spreadsheet and automatic type guessing is a risk.

## Steps
1. Inspect the raw file as text before any spreadsheet opens it: encoding, delimiter, quoting, header, decimal separator and a sample of date strings.
2. Mark columns that are identifiers, not quantities: postcodes, phone numbers, account or part codes, long order numbers. These must be text.
3. Determine date order from evidence, such as a day above 12. If none exists, ask the source.
4. Import through the application's data import dialog and set column types explicitly; do not double-click the file. Programmatically, read with all columns as strings (pandas `dtype=str, keep_default_na=False`), then convert chosen ones.
5. Watch for values such as "NA" (a real country code), "1E5" style codes, and text resembling dates.
6. Neutralise untrusted cells that begin with `=`, `+`, `-`, `@`, tab, carriage return or line feed, or a full-width form of those four symbols, so they are not run as formulas, while keeping genuine negative numbers numeric.
7. Save as .xlsx to retain types.
8. Compare row and column counts and spot-check identifier lengths and min and max dates against the raw text.

## Watch out for
- Excel keeps about 15 significant digits, so longer numbers are permanently altered if read as numeric. Reformatting afterwards does not restore them.
- Re-saving as CSV can change date and number presentation according to locale.
- A UTF-8 file without a byte order mark may display accented text wrongly in some applications.
- Naive line counts mislead when quoted fields contain newlines.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Sampled identifiers and dates match the raw file character for character or by confirmed meaning, and counts agree.
