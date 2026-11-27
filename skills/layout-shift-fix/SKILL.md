---
name: layout-shift-fix
version: 1.0.0
description: >
  Find and remove unexpected layout shifts, including those that happen after load, by identifying the moved elements. Use when content jumps while reading or tapping, or CLS fails.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - performance
  - web-vitals
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
  - computer.scroll
metadata:
  source: library
  library_id: layout-shift-fix
  official: true
  domain: frontend
  security_flags: []
---

# Layout Shift Fix

## When to use
Users mis-tap because things move, or cumulative layout shift exceeds the usual good value of 0.1.

## Steps
1. Log shifts with their sources by running a `PerformanceObserver` for `layout-shift` entries with `buffered: true`, ignoring those with `hadRecentInput`. Keep it running while scrolling and navigating, not only during load.
2. Throttle the network and use a cold cache so late resources actually arrive late.
3. For each source, find what changed above or around it. The element that moved is often not the cause.
4. Media and embeds: set dimensions or `aspect-ratio`.
5. Ads, banners, consent bars and injected promos: reserve space of the common size, or overlay them instead of pushing content.
6. Async data: make placeholders match final height, including the empty and error results.
7. Fonts: adjust fallback metrics so the swap keeps line breaks.
8. Animations: move with `transform` rather than `top`, `height` or margins.
9. Account for scrollbar appearance with `scrollbar-gutter: stable` where it shifts centred layouts.
10. Re-run the observer over the same script of actions at phone and desktop widths.

## Watch out for
- A lab tool that only loads the page misses shifts caused by scrolling or late timers.
- Reserving a fixed height that is wrong for some content swaps one jump for another.
- Content inserted a long delay after a click no longer counts as user-initiated.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The scripted session at both widths records a total below target, and each previously logged shift source is fixed or explicitly accepted.
