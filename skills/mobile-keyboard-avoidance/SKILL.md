---
name: mobile-keyboard-avoidance
version: 1.0.0
description: >
  Keep focused inputs and submit buttons visible above the on-screen keyboard in iOS, Android and cross-platform screens. Use when the keyboard covers fields, composers or buttons.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - mobile
  - forms
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: mobile-keyboard-avoidance
  official: true
  domain: frontend
  security_flags: []
---

# Mobile Keyboard Avoidance

## When to use
Login, checkout or chat screens are unusable while the keyboard is open on some devices.

## Steps
1. Identify the stack and screen type: scrolling form, pinned bottom composer, sheet or dialog. Each needs different handling.
2. Search for stacked existing workarounds (keyboard height constants, manual offsets, multiple avoiding wrappers) and remove them before adding one.
3. SwiftUI adjusts safe areas automatically; check for `ignoresSafeArea` that disables it and use `safeAreaInset(edge: .bottom)` for composers. UIKit: constrain to `view.keyboardLayoutGuide` where the deployment target allows.
4. Android: use `adjustResize` with IME insets (`imePadding()` in Compose) and make the form scrollable.
5. React Native: `KeyboardAvoidingView` behaves differently per platform, so verify each and account for header height; use the project's keyboard library if present. Set `keyboardShouldPersistTaps="handled"` so the first tap on a button works.
6. Flutter: check `resizeToAvoidBottomInset`, make content scrollable and use `MediaQuery.viewInsetsOf` for custom pinned elements.
7. Set keyboard type, return key action and next-field focus order, and mark fields for autofill.
8. Provide a way to dismiss numeric keyboards that lack a return key.
9. Test the smallest screen, landscape, a third-party or tall keyboard, hardware keyboard and a floating or split tablet keyboard.

## Watch out for
- Keyboard height varies and changes while open, for instance when a suggestion bar appears.
- Applying both window resize and manual padding leaves a double gap.
- A focused field can be visible while its validation error stays hidden below.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
On each target platform every field, its error text and the primary action are visible or reachable by scrolling with the keyboard open, and dismissing restores the layout.
