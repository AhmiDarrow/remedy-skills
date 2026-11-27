---
name: motion-design-spec
version: 1.0.1
description: >
  Specify interface motion per interaction: purpose, trigger, properties, duration, easing, interruption and reduced-motion behaviour. Use when animations need defining before build or feel inconsistent.
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
metadata:
  source: library
  library_id: motion-design-spec
  official: true
  domain: design
  security_flags: []
---

# Motion Design Spec

## When to use
Designers and developers need exact, shared rules for how things move.

## Steps
1. `grep` for transitions, keyframes and animation library calls, and note current durations and curves.
2. For each proposed animation name its job: show where something came from, confirm an action, draw attention or show progress. Drop those with none, especially on actions repeated all day.
3. Define a small token set for durations and easing, reusing existing ones. As a starting point to tune by eye, small feedback sits near 100 to 200 ms and larger surface transitions near 200 to 400 ms.
4. Use deceleration for entering, acceleration for leaving and ease-in-out for movement on screen. Reserve linear for continuous progress or rotation. Define spring settings if springs are used.
5. Write a table per interaction: trigger, element, properties with start and end values, duration, delay, easing, origin.
6. Describe choreography: order, overlap and a cap on stagger so long lists do not make people wait.
7. Specify interruption: repeated clicks, reversal midway, navigation during motion. Input should not be blocked by decoration, and logic should not depend only on an end event.
8. Give the reduced-motion version for each: replace large travel, zoom, parallax and spin with a short fade or instant change, keeping the information.
9. Prefer transform and opacity, flag animations of layout properties, and plan a check on a modest device.
10. Provide a prototype or precise code values and acceptance checks.

## Watch out for
- Motion as the only signal that something changed.
- Auto-playing movement over five seconds without pause, stop or hide, or anything flashing more than three times a second.
- `will-change` applied everywhere consumes memory.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each animation has a purpose, complete values, interruption behaviour and a reduced-motion version, uses shared tokens, and performance checks are run or listed as pending.
