---
name: css-container-queries
version: 1.0.0
description: >
  Make components respond to the space they are given using CSS container queries instead of viewport breakpoints. Use when a card or widget breaks in a sidebar, split view or dashboard slot.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - responsive
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: css-container-queries
  official: true
  domain: frontend
  security_flags: []
---

# Css Container Queries

## When to use
The same component appears in wide and narrow slots and viewport media queries cannot tell them apart.

## Steps
1. List the slots the component occupies and measure the inline sizes at which its content actually stops working. Those are the breakpoints, not device widths.
2. Choose the wrapper that receives its width from the parent. Set `container-type: inline-size` and a `container-name` on it.
3. Write the narrow arrangement as the base style, then add `@container name (min-width: 28rem)` rules for roomier ones.
4. Remember that a query styles descendants of the container, never the container itself; add a wrapper if the root must change.
5. Replace viewport units inside the component with container units such as `cqi` where sizes should follow the slot.
6. Delete the obsolete media queries and any `.in-sidebar` override classes the component no longer needs.
7. Check browser support against the project's browserslist; the narrow base style is the fallback.
8. Resize each slot in dev tools through every threshold.

## Watch out for
- Size containment means the container's width cannot come from its children. Applied to a shrink-to-fit element (inline-block, an `auto` grid track, a float, a flex item with no basis) it can collapse to zero.
- `container-type: size` also removes content-based height, so it needs an explicit height.
- Without a name, a query matches the nearest ancestor container, which may be one added later by someone else.
- Custom properties cannot be used inside the query condition.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The component shows the right arrangement in every slot at one viewport width, none collapses, and no parent-specific override classes remain.
