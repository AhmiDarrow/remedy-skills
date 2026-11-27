---
name: spacing-layout-grid
version: 1.0.1
description: >
  Define a spacing scale, layout grid, container widths and usage rules, and apply them to real screens. Use when margins and gaps are arbitrary or a new interface needs layout foundations.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ui
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: spacing-layout-grid
  official: true
  domain: design
  security_flags: []
---

# Spacing Layout Grid

## When to use
Layouts feel uneven because every screen picks its own numbers.

## Steps
1. `grep` styles for margin, padding, gap, width and max-width values and count them. Check whether a framework already supplies a scale; extend that instead of adding another.
2. Choose a base unit, often 4 px with most steps on multiples of 8, expressed in the project's units.
3. Build a short scale with steps spaced further apart as they grow. Name the tokens and say what each is for.
4. State the proximity rule: space inside a group is smaller than space between groups, at every level.
5. Separate component padding and gaps from page rhythm, and define density variants only if a real case needs them.
6. Define layout primitives (stack, row, cluster, sidebar, card grid) that own spacing through `gap`, so children avoid outer margins.
7. Define page grid per width range: columns, gutters, outer margins, and which spans common layouts use. Not every component needs the page columns.
8. Set maximum widths by content: a readable measure for prose, wider containers for tables and dashboards.
9. Apply to two or three different real screens, including a dense one, and adjust the scale where it fails.
10. Map old values to tokens, listing optical exceptions with reasons, and propose a lint check for new raw values.

## Watch out for
- Mechanical rounding of every value that breaks alignment or shrinks targets.
- Fixed heights on text containers, which clip when text grows.
- A scale with so many near-equal steps that choices stay arbitrary.
- Borders and line height can make mathematically equal spacing look unequal.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tokens, grid and container rules are written with usage guidance, demonstrated on real screens, checked at narrow and wide sizes, and remaining exceptions are listed.
