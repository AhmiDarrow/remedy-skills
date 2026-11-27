---
name: android-predictive-back
version: 1.0.0
description: >
  Migrate Android back handling to the supported back callbacks so predictive back gestures animate and behave correctly. Use when onBackPressed overrides or custom back logic misbehave.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - android
  - navigation
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: android-predictive-back
  official: true
  domain: frontend
  security_flags: []
---

# Android Predictive Back

## When to use
An app overrides `onBackPressed` or listens for `KEYCODE_BACK`, or newer Android versions skip its back logic.

## Steps
1. `grep` for `onBackPressed`, `KEYCODE_BACK`, `OnBackPressedCallback`, `BackHandler` and framework or cross-platform back hooks.
2. For each, state what it does: close a drawer, step a wizard, confirm discard, navigate a web view, exit.
3. Delete handlers that duplicate what the navigation library or system already does.
4. Replace the rest with AndroidX `OnBackPressedDispatcher` callbacks, or `BackHandler` and the predictive back APIs in Compose.
5. Drive each callback's enabled state from UI state before the gesture begins, for example enabled only while the form is dirty or the drawer open. The system must know in advance who handles back.
6. Do not decide inside the callback to pass back through by disabling and re-dispatching as a routine pattern.
7. Add progress-driven animation only where the surface benefits, handling cancel.
8. Set `android:enableOnBackInvokedCallback` to match the target SDK. For apps targeting API 36 on Android 16 or later, predictive back is on by default, `onBackPressed` is not called and `KEYCODE_BACK` is not dispatched; setting the attribute to `false` is only a temporary opt-out. Check the platform notes for newer levels.
9. Update library versions that need it and test with gesture and button navigation, including cancelling halfway.

## Watch out for
- An always-enabled root callback removes the back-to-home preview and can trap users.
- Using back to log analytics or save data misses other exits; save on lifecycle events.
- Exit confirmation toasts on the home screen fight the platform gesture.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No legacy interception remains, each listed behaviour works with gesture and buttons, cancelled gestures change nothing, and the root screen previews returning home.
