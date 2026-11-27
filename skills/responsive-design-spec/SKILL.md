---
name: responsive-design-spec
version: 1.0.1
description: >
  Specify how screens adapt across widths, zoom and input types: breakpoints, content priority, reflow rules and component behaviour. Use when designs exist for one size and developers must guess the rest.
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
  - grep
  - glob
metadata:
  source: library
  library_id: responsive-design-spec
  official: true
  domain: design
  security_flags: []
---

# Responsive Design Spec

## When to use
Responsive behaviour needs defining before or alongside implementation. Fixing already broken CSS is a separate job.

## Steps
1. `grep` the project for existing breakpoints, container queries, grid settings and layout components. Reuse them and flag conflicts.
2. Ask which devices and windows matter, using analytics if provided, and include split screen, landscape phones and very wide monitors.
3. For each key screen rank tasks and content. Everything needed for a task stays reachable at every width.
4. Start from the narrow single column, keeping source order meaningful, then add arrangements where content starts to break, not at device names.
5. Write ranges with explicit boundaries. For each region state whether it reflows, stacks, resizes, scrolls, collapses behind a control or moves.
6. Decide per component whether it responds to the viewport or its container.
7. Define the hard ones: navigation, tables, filters, toolbars, dialogs, forms, charts, media crops and sticky elements.
8. Treat input separately from width: detect hover and pointer capability, give touch targets room, and never hide a function behind hover.
9. Require reflow at 320 CSS px wide without two-dimensional scrolling, except content that needs it such as data tables, maps or diagrams. Check 200% text enlargement, long translations, on-screen keyboard and safe areas.
10. Give a behaviour table per screen, image sizing rules and test widths just below and above each boundary.

## Watch out for
- Visual reordering by CSS that no longer matches focus and reading order.
- Hidden content still downloaded, or still focusable when off screen.
- Full-height panels that trap content when the screen is short.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each key screen has behaviour for every range and special condition, hard components are defined, nothing essential is unreachable, and a test list covers the boundaries.
