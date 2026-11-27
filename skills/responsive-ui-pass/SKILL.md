---
name: responsive-ui-pass
version: 1.0.1
description: >
  Find and fix layout breakage across widths, zoom and long content, from overflow and clipped buttons to unreachable menus. Use when a page breaks on phones, tablets or narrow windows.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - computer.navigate
  - computer.snapshot
  - computer.screenshot
  - computer.window
metadata:
  source: library
  library_id: responsive-ui-pass
  official: true
  security_flags: []
---

# Responsive Ui Pass

## When to use
Implemented screens break at some sizes.

## Steps
1. List target routes and states, including dialogs, tables, forms, logged-in views and errors. Read the project's breakpoints and check the viewport meta tag does not block zoom.
2. Sweep continuously from 320 CSS pixels to wide, not only at device presets. Note the exact width where each break starts and screenshot it. If you cannot render the page, say findings come from code only.
3. For sideways scroll, find the overflowing element in developer tools. Hiding overflow on `body` only conceals it.
4. Fix the cause: `min-width: 0` on shrinking flex or grid children, `minmax(0, 1fr)` tracks, wrapping rows, `max-width: 100%` on media, `overflow-wrap` for long strings, and removal of fixed widths or heights around text.
5. Give wide tables and code their own labelled, keyboard-scrollable region, or a deliberate stacked layout.
6. Check sticky bars, drawers and modals at short heights and landscape: every action must be reachable by scrolling.
7. Stress with long names, translated text, large numbers, empty content and 200% zoom.
8. Check touch: no hover-only actions and adequately sized, spaced targets.
9. After each fix, re-check neighbouring widths and the desktop layout.

## Watch out for
- Hiding content or actions on small screens removes features people need.
- Reordering with CSS `order` or grid placement leaves keyboard order unchanged and confusing.
- Adding a breakpoint per phone model instead of where content breaks.
- Window emulation is not a real device: keyboard, safe areas and browser toolbars need a device check.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Scoped screens have no unintended horizontal scroll from 320 pixels up, primary actions are reachable, and remaining gaps and untested devices are listed.
