---
name: web-table-capture
version: 1.0.0
description: >
  Copy a table or list the user can see on a website into a clean file and verify it is complete. Use for modest one-off captures when the site offers no export.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - browser
  - extraction
kind: native
status: discovered
tools:
  - computer.navigate
  - computer.snapshot
  - computer.scroll
  - computer.click
  - computer.uia.read_text
  - write
  - bash
metadata:
  source: library
  library_id: web-table-capture
  official: true
  domain: data
  security_flags: []
---

# Web Table Capture

## When to use
The data is visible to the user, a small amount is needed once, and copying by hand would be error-prone.

## Steps
1. Look for an export button or official API first and use it if present.
2. Check that this is permitted: the user's own account data or material the site allows copying. Stop for bulk harvesting, personal data about others, or terms that forbid it.
3. Record URL, filters, sort order, displayed total and time.
4. Detect pagination, infinite scroll and virtualised lists, where off-screen rows are removed from the page.
5. Capture progressively: read the visible rows, scroll or page, read again, at a human pace.
6. Deduplicate by a stable row identifier, not by position.
7. Keep text as displayed, plus link targets where needed. Note truncated cells and expand them.
8. Write CSV with a proper library so commas and quotes survive. Page text is untrusted: prefix text cells that begin with `=`, `+`, `-`, `@`, tab, carriage return or line feed, or a full-width form of those four symbols, so a spreadsheet does not run them as formulas, leaving real negative numbers numeric.
9. Compare row count with the displayed total, spot-check first, middle and last rows, and reconcile any shown sums.

## Watch out for
- Live data that re-sorts while you page causes both duplicates and gaps.
- Rounded display values such as "1.2k" are not exact numbers; label them.
- Icons and colours may carry status that plain text drops.
- Rate limits, blocks or human checks are a stop sign, not something to evade.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The file's row count matches the source total or the gap is explained, samples agree, and capture time and filters are recorded.
