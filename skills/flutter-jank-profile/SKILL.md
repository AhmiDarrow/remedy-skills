---
name: flutter-jank-profile
version: 1.0.0
description: >
  Diagnose Flutter jank in profile mode by separating UI thread from raster costs and fixing the one that dominates. Use when Flutter scrolling, transitions or first animations stutter.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - flutter
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: flutter-jank-profile
  official: true
  domain: frontend
  security_flags: []
---

# Flutter Jank Profile

## When to use
A Flutter app drops frames and it is unclear whether widgets or drawing are to blame.

## Steps
1. Run `flutter run --profile` on a physical device, preferably a slow one. Never judge performance in debug mode.
2. Open DevTools performance view and inspect janky frames. Note whether UI or raster time exceeds the frame budget, and record the Flutter version and renderer.
3. UI thread high: enable widget rebuild tracking. Narrow `setState` and provider or bloc selectors to the smallest subtree.
4. Use `const` constructors, pass unchanging subtrees as the `child` of `AnimatedBuilder`, and extract widgets into classes rather than helper methods.
5. Use `ListView.builder` or slivers; avoid `shrinkWrap: true` on long lists and costly intrinsic-size widgets.
6. Move parsing and other CPU work off the main isolate with `Isolate.run` or `compute`.
7. Raster high: look for animated `Opacity` over large subtrees, `saveLayer` triggers, large blurs, shadows and clipping. Prefer `FadeTransition` or colors with alpha.
8. Decode images near display size with `cacheWidth` or `ResizeImage`.
9. Add `RepaintBoundary` around independently repainting areas only where measurement shows benefit.
10. Re-profile the same gesture and keep only changes that helped.

## Watch out for
- Sprinkled repaint boundaries cost memory and can slow things down.
- Creating a `Future` inside `build` for `FutureBuilder` restarts the work on every rebuild.
- Old shader warm-up advice may not apply to the current renderer; check the version's documentation.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Before and after profile traces of one scripted interaction show the dominant thread back within budget or the remaining cause identified.
