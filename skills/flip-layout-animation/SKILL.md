---
name: flip-layout-animation
version: 1.0.0
description: >
  Animate reordering, expanding and shared-element changes smoothly with the FLIP technique instead of animating layout. Use when items jump on sort or filter, or height animations stutter.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - animation
  - performance
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
  library_id: flip-layout-animation
  official: true
  domain: frontend
  security_flags: []
---

# Flip Layout Animation

## When to use
Cards reorder, a thumbnail grows into a detail panel, or a list closes a gap, and the change should be continuous.

## Steps
1. Check for an installed animation library with layout animation, or the View Transitions API, before hand-writing it.
2. Give each moving item stable identity so the same DOM node or a matched pair exists before and after.
3. First: record `getBoundingClientRect()` for all affected items.
4. Last: apply the DOM change and measure again, in the same frame before paint (a layout effect in component frameworks).
5. Invert: apply the transform that makes each item look like its old position, using translate and, if size changed, scale with `transform-origin: top left`.
6. Play: animate that transform to identity with the Web Animations API.
7. Batch all reads before all writes.
8. For interruptions, measure the current on-screen position before cancelling the running animation, and start from there.
9. Handle entering and leaving items separately: fade in new ones; take leaving ones out of flow while keeping their position.
10. Under reduced motion, apply the change immediately or crossfade.

## Watch out for
- Scaling a container distorts text, borders and radius; counter-scale children, crossfade, or animate `clip-path` instead.
- Scroll between the two measurements offsets viewport coordinates.
- Measuring while a previous transform is applied gives the visual box, not the layout box.
- Removed items that stay focusable or announced during exit confuse keyboard users.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Rapid repeated sorting animates from visible positions without jumps, a trace shows no per-frame layout work, and reduced motion removes the movement.
