---
name: woodworking-cut-list
version: 1.0.0
description: >
  Turn a furniture or shelving idea into a cut list and board layout with kerf, grain and real stock sizes. Use before buying timber or sheet material for a build.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - hobby
  - woodworking
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: woodworking-cut-list
  official: true
  domain: personal
  security_flags: []
---

# Woodworking Cut List

## When to use
A build needs a materials list that will actually assemble.

## Steps
1. Get overall size, the space it must fit (measured at several points), load it must carry, units, material and joinery.
2. Measure real stock thickness and sheet size. Nominal timber sizes differ from actual ones.
3. List each part with quantity, length, width, thickness and grain direction. Derive internal parts from joinery: butt joints subtract mating thickness, grooves add their depth to each end.
4. Check the arithmetic: parts plus thicknesses across each axis must equal the outer size.
5. Add blade kerf between cuts, using the measured blade, plus a trim allowance for rough edges.
6. Lay out parts on stock with long and large pieces first, respecting grain. A quick script can check totals.
7. Order cuts so matching parts share one fence setting, and leave fitted parts such as backs, doors and drawers to be cut after dry assembly.
8. List hardware with its clearances, taken from the maker's sheet, and offcut waste.

## Watch out for
- Area totals showing enough material when shapes cannot fit.
- Solid wood moves across the grain; fixed cross-grain joints can split.
- Long shelves sagging or tall units tipping; anchor tall furniture to the wall.
- Narrow or small cuts on power tools without push sticks and guards.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Dimensions reconcile on all axes and every part has a place on listed stock including kerf.
