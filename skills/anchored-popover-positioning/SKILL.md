---
name: anchored-popover-positioning
version: 1.0.0
description: >
  Build menus, tooltips and popovers that stay on screen, flip near edges and dismiss correctly. Use when a floating panel is clipped, runs off the window or will not close properly.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - overlays
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
  - computer.screenshot
metadata:
  source: library
  library_id: anchored-popover-positioning
  official: true
  domain: frontend
  security_flags: []
---

# Anchored Popover Positioning

## When to use
A dropdown near the bottom edge is cut off, or each overlay in the app positions and closes itself differently.

## Steps
1. `grep` for an existing positioning helper or library and route all overlays through one of them.
2. Choose semantics first: tooltip (describes a control, no interactive content), menu (commands), listbox (selection), or non-modal dialog (form or links). Each has different keyboard behaviour.
3. Use the `popover` attribute for top-layer rendering and light dismiss where supported. `popover="auto"` closes on Escape and outside click; `manual` does neither.
4. Position with CSS anchor positioning if the supported browsers have it, with fallbacks for flipping; otherwise use the installed library's offset, flip, shift and size steps.
5. State the placement rules: preferred side, flip when it does not fit, slide along the edge, then limit height and scroll internally.
6. Update on scroll of any ancestor, window resize and content size change; stop observing on close.
7. Manage focus: menus move focus in and return it to the trigger; tooltips never take focus, show on focus as well as hover, stay while the pointer is over them and close on Escape.
8. Test the trigger in all four corners, in a narrow window, at 200% zoom, inside a scroll container and inside a modal.

## Watch out for
- `title` attributes are invisible to touch and most keyboard users; do not use them for needed information.
- Outside-click handlers on `click` can close and immediately reopen when the trigger itself is clicked.
- Measuring before content or fonts load gives a position that overflows a frame later.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
In all corner, narrow and zoomed cases the whole panel is reachable on screen, Escape and outside click behave as specified, and focus returns to the trigger.
