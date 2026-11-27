---
name: android-edge-to-edge
version: 1.0.0
description: >
  Adapt Android screens to edge-to-edge display by handling system bar, cutout and keyboard insets correctly. Use when content hides under bars after raising targetSdk or enabling edge-to-edge.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - android
  - layout
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - bash
metadata:
  source: library
  library_id: android-edge-to-edge
  official: true
  domain: frontend
  security_flags: []
---

# Android Edge To Edge

## When to use
Toolbars slide under the status bar, bottom buttons sit under gesture navigation, or the keyboard covers fields.

## Steps
1. Read `targetSdk`. Apps targeting Android 15 (API 35) are drawn edge-to-edge by default on Android 15 and later. The `windowOptOutEdgeToEdgeEnforcement` opt-out is disabled for apps targeting API 36 on Android 16 devices, so do not rely on it. Call `enableEdgeToEdge()` for consistent behaviour on older releases.
2. List every window surface: activities, dialogs, bottom sheets, full-screen players, splash and third-party screens.
3. In Compose with Material 3, pass `Scaffold`'s content padding to the content. Elsewhere use `WindowInsets.safeDrawing`, `systemBarsPadding()`, `navigationBarsPadding()` or `imePadding()` where each applies.
4. For scrolling lists put insets in `contentPadding`, so content scrolls behind bars yet the last item clears them.
5. In Views use `ViewCompat.setOnApplyWindowInsetsListener`, reading `systemBars()`, `displayCutout()` and `ime()`, adding to the original padding rather than accumulating on each callback.
6. Let backgrounds extend under bars while text and touch targets stay inside safe areas.
7. Set status and navigation icon appearance to contrast with what is behind them in both themes.
8. For keyboard handling set `windowSoftInputMode` to `adjustResize` and apply IME insets.
9. Test gesture and three-button navigation, landscape with a cutout, keyboard open and an older API level.

## Watch out for
- Hard-coded status bar heights are wrong on many devices.
- Applying the same inset at both parent and child doubles the gap unless consumption is handled.
- Gesture areas can swallow swipes near edges even when content is visible.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
On both navigation modes, both orientations and with the keyboard open, no control or text is obscured and no doubled padding appears on any listed surface.
