---
name: data-table-build
version: 1.0.0
description: >
  Build a usable data table with correct semantics, sorting, filtering, selection and narrow-screen behaviour. Use when creating or repairing an admin or report grid that users work in daily.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - components
  - ux
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: data-table-build
  official: true
  domain: frontend
  security_flags: []
---

# Data Table Build

## When to use
A list of records needs comparing and acting on, or the current table is a pile of divs that breaks with real data.

## Steps
1. Ask what users do with it: find one row, compare a column, or act on many. That decides columns, default sort and density.
2. Start from a real `table` with `caption`, `th scope="col"` and row headers. Use the grid role only if cells need arrow-key navigation and you will implement all of it.
3. Right-align numeric columns, use tabular figures, put units in headers, and format by locale.
4. Make sort a button inside the header and set `aria-sort` on the sorted column. Sort by raw values with a stable tiebreaker and defined placement for blanks.
5. Decide client or server operations from data size. With server paging, sorting and filtering must happen on the server too.
6. Show active filters as removable items with the result count, and keep them in the URL.
7. Specify selection: does the header checkbox select the page or all matches? Say which in words with the count, and clear or preserve selection explicitly when filters change.
8. Handle width by horizontal scroll with a sticky identifying column, or column priority; use stacked cards only when comparison does not matter.
9. Design first-load, refreshing, empty, filtered-empty and error rows.

## Watch out for
- A bulk action that silently includes rows hidden by filters or other pages is destructive; confirm with the exact count.
- Making the entire row clickable breaks text selection and nested controls; keep a real link in the primary cell.
- Setting `display: block` on table elements for mobile can strip table semantics in some browsers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
With realistic long and empty values the table sorts, filters and selects as specified, selection counts match what a bulk action receives, and headers are announced by a screen reader.
