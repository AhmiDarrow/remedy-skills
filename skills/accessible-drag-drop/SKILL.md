---
name: accessible-drag-drop
version: 1.0.0
description: >
  Give drag-and-drop reordering, kanban and canvas moves a keyboard, screen reader and single-pointer alternative. Use when adding draggable UI or when dragging is the only way to do something.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - accessibility
  - interaction
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.key
  - computer.snapshot
metadata:
  source: library
  library_id: accessible-drag-drop
  official: true
  domain: frontend
  security_flags: []
---

# Accessible Drag Drop

## When to use
Items can only be moved by dragging, or a drag library is in place with default announcements and no touch alternative.

## Steps
1. List every outcome dragging produces: reorder, move between groups, resize, assign, upload.
2. Provide a non-drag route to each that works with single clicks or taps, such as Move up and down buttons or a Move to menu with destination and position. WCAG 2.2 asks for a single-pointer alternative unless dragging is essential; keyboard support alone does not satisfy it.
3. Add keyboard moving: pick up from a labelled handle, arrows to move, Enter or Space to drop, Escape to cancel back to the origin.
4. Announce pick-up, each position change and drop in human terms: item name, column, position 2 of 5. Replace library defaults that read internal ids.
5. Keep focus on the moved item after the drop and scroll it into view.
6. Prefer an installed library with keyboard sensors; native HTML drag and drop has poor touch and keyboard support.
7. On touch, separate drag from scroll using a handle or press delay, with `touch-action: none` only on the handle.
8. Show insertion position, invalid targets and auto-scroll near edges.
9. Persist optimistically and revert with a message on failure.

## Watch out for
- `aria-grabbed` and `aria-dropeffect` are deprecated and do not make anything accessible.
- Re-rendering with index keys after a move loses focus.
- `touch-action: none` on whole cards makes the list impossible to scroll on phones.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every listed outcome has been completed once by keyboard, once by single taps and once by drag, with correct spoken positions and a working cancel.
