---
name: react-native-list-perf
version: 1.0.0
description: >
  Fix slow or blank-flashing long lists in React Native by tuning FlatList or a recycling list on a release build. Use when scrolling stutters or white gaps appear while scrolling.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - react-native
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
  library_id: react-native-list-perf
  official: true
  domain: frontend
  security_flags: []
---

# React Native List Perf

## When to use
A feed or chat list is choppy, shows blank areas, or grows slower as items load.

## Steps
1. Reproduce on a real low-end Android device in a release build. Development mode distorts timings. Note the React Native version and whether the new architecture is enabled.
2. Watch JavaScript and UI thread frame rates and profile to see whether the cost is rendering, image decoding or other JavaScript work.
3. Check that the list is not nested in a same-direction `ScrollView`, which makes it render everything.
4. Provide a stable `keyExtractor`, keep `renderItem` and its props referentially stable, and memoise rows, unless the React compiler already handles it.
5. Simplify rows: fewer nested views, precomputed strings and no heavy work during render.
6. For fixed sizes supply `getItemLayout`.
7. Tune `initialNumToRender`, `maxToRenderPerBatch` and `windowSize` one at a time, recording the effect. Smaller windows save memory but show more blanks.
8. Request images at display size and use a caching image component.
9. If still inadequate, evaluate a recycling list library compatible with the version. Reset row local state when a recycled row gets a new item.
10. Move scroll-linked animation to the native or UI thread.

## Watch out for
- `console.log` calls left in release builds consume the JavaScript thread.
- Index keys cause wrong images and state in recycled or reordered rows.
- `removeClippedSubviews` can leave content missing in some layouts; verify visually.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The same scroll on the same device in release mode shows measurably steadier frames and fewer blanks, with row state correct after fast scrolling and reordering.
