---
name: animation-jank-debug
version: 1.0.0
description: >
  Diagnose stuttering web animations and scrolling by locating layout, paint or main-thread costs in a frame trace. Use when an animation drops frames, especially on phones.
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
metadata:
  source: library
  library_id: animation-jank-debug
  official: true
  domain: frontend
  security_flags: []
---

# Animation Jank Debug

## When to use
A drawer, carousel, parallax effect or scroll feels choppy.

## Steps
1. Reproduce on a weak or CPU-throttled device and record a trace of just the animation. Note the display refresh rate; the frame budget is about 16.7 ms at 60 Hz and half that at 120 Hz.
2. Classify the long frames: script, style recalculation, layout, paint or compositing.
3. Find what is animated. Replace `width`, `height`, `top`, `left` and margins with `transform` and `opacity` where the design allows.
4. Check forced reflow: reading geometry after writing styles within a loop. Read first, then write.
5. Turn on paint flashing. Large blurred shadows, `filter`, `backdrop-filter` and gradients repainted each frame are common culprits; fade a pre-rendered layer's opacity instead.
6. Inspect layers. Add `will-change` only to the few elements that need it, around the time of animation.
7. Replace scroll event handlers with CSS scroll-driven animations or `IntersectionObserver`, and make touch and wheel listeners passive when they do not cancel.
8. Drive JavaScript animation with `requestAnimationFrame` using elapsed time, not a per-frame increment or `setInterval`.
9. Re-record the same interaction and compare.

## Watch out for
- Compositor-only animation can still stutter if layer count exhausts graphics memory on phones.
- Animating a CSS variable used by many descendants restyles all of them each frame.
- Per-frame increments run twice as fast on 120 Hz screens.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Before and after traces on the same throttled setup show the identified cost gone and dropped frames reduced, with motion duration consistent across refresh rates.
