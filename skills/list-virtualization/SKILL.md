---
name: list-virtualization
version: 1.0.0
description: >
  Add windowed rendering to very long lists or grids without breaking scrolling, search, focus or accessibility. Use when thousands of rows make a view slow to open or scroll.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - performance
  - components
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
  - computer.scroll
metadata:
  source: library
  library_id: list-virtualization
  official: true
  domain: frontend
  security_flags: []
---

# List Virtualization

## When to use
Profiling shows DOM size or row rendering dominates a long list.

## Steps
1. Confirm the bottleneck by profiling with realistic data. Try pagination or `content-visibility: auto` first if they meet the need.
2. List what currently relies on all rows existing: browser find, select all and copy, anchor links, printing, tests that query by text, keyboard navigation.
3. Use an installed or well-established virtualizer rather than writing the math.
4. Choose fixed, estimated or measured row height. For variable rows, measure actual elements and re-measure on width change, image load and expansion.
5. Key rows by stable id. Lift row state (checked, expanded, draft text) out of the row component, because rows unmount.
6. Set modest overscan and tune it by scrolling quickly on a slow device.
7. Keep the focused row mounted, and make arrow, Page, Home and End keys scroll the target into view before focusing it.
8. Convey true totals with `aria-setsize` and `aria-posinset`, or `aria-rowcount` and `aria-rowindex` for grids.
9. Provide in-app search and export to replace lost browser features.
10. Re-profile and test prepending items, filtering and resizing.

## Watch out for
- A scroll container without a bounded height renders every row and virtualizes nothing.
- Index keys make row state and images flash onto other items.
- Estimates far from reality make the scrollbar jump, especially when scrolling upward.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Mounted row count stays roughly constant at any data size, profiling shows the improvement, and each item from the dependency list works or has an agreed replacement.
