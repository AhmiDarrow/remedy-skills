---
name: pdf-table-extraction
version: 1.0.0
description: >
  Get tables out of a PDF into CSV or a spreadsheet and prove the numbers survived. Use when figures are locked in a report, statement or datasheet.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - pdf
  - extraction
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: pdf-table-extraction
  official: true
  domain: data
  security_flags: []
---

# Pdf Table Extraction

## When to use
The user needs rows and columns they can calculate with.

## Steps
1. First look for the same data as a published CSV or spreadsheet; it removes extraction risk.
2. Render the relevant pages and note ruled versus borderless layout, merged headers, multi-line cells and page breaks.
3. Use an installed table library such as pdfplumber or Camelot, or `pdftotext -layout` for simple grids. Run Python with `-I` on downloaded files, from a directory separate from them.
4. Line-based detection suits ruled tables; whitespace-based detection suits borderless ones. Adjust one setting at a time and look at the result.
5. Flatten multi-level headers into explicit column names. Stitch continued tables and drop repeated header rows.
6. Keep a raw string version, then convert types: thousands separators, parentheses as negatives, dashes, footnote markers, percent signs.
7. Reconcile: recompute row and column totals against printed ones and count rows against the page.
8. Spot-check at least ten cells, including the first and last of each page, and save source page numbers in a column.

## Watch out for
- An empty cell can shift every later value one column left while still looking tidy.
- A dash may mean zero, not applicable or suppressed. Read the table's legend.
- "In thousands" in a caption changes every value by a factor of 1000.
- Totals that differ by rounding are expected; larger differences mean an extraction or source error to report.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Totals reconcile or discrepancies are listed cell by cell, and each row can be traced to its page.
