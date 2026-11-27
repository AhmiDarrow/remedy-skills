---
name: csv-data-cleanup
version: 1.0.1
description: >
  Profile and clean a CSV or TSV file with a re-runnable script, keeping the original and reporting every changed, rejected and doubtful row. Use when delimited data is messy before analysis or import.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - csv
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: csv-data-cleanup
  official: true
  security_flags: []
---

# Csv Data Cleanup

## When to use
A delimited file has inconsistent formats, blanks, duplicates or broken rows.

## Steps
1. Keep the source read-only. Record its size, a hash and the first lines. Ask what the cleaned file feeds and which columns identify a row.
2. Determine encoding, delimiter, quote character and header from the bytes and a sample. Parse with a real CSV parser, never by splitting lines or commas.
3. Load every column as text so IDs keep leading zeros and codes like "NA" survive (in pandas, `dtype=str, keep_default_na=False`).
4. Profile: parsed record count, rows with wrong field counts, and per column the blanks, distinct values, common patterns, min and max, and surrounding or invisible whitespace.
5. Write the rules before applying them: which tokens mean missing in which column, category mappings, date input formats and output ISO 8601, decimal and thousands separators, units and time zones. Ask about ambiguous cases such as 03/04/2026.
6. Implement the rules in a script. Convert column by column; a value that fails goes to a rejects file with row number and reason, not to blank.
7. Treat exact duplicate rows separately from rows sharing a business key but disagreeing. List conflicts for a decision on which wins.
8. Flag outliers for review rather than deleting them.
9. Write new cleaned, rejects and report files. Reconcile: input records = output + rejected + removed duplicates. Compare key totals before and after.
10. Rerun the script on the original and confirm identical output.

## Watch out for
- Quoted newlines make `wc -l` disagree with the record count.
- Filling missing numbers with zero changes averages and totals.
- Free text starting with `=`, `+`, `-`, `@`, tab or carriage return can run as a formula when opened in a spreadsheet; neutralise it in files meant for that.
- Sample rows in your report may contain personal data; mask them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A script reproduces the cleaned file from the untouched source, the row counts reconcile, rules and rejects are written out, and unresolved ambiguities are listed.
