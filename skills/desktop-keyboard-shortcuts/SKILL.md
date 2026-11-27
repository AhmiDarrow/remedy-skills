---
name: desktop-keyboard-shortcuts
version: 1.0.0
description: >
  Design and implement desktop or web app keyboard shortcuts with platform conventions, scopes and layout safety. Use when adding hotkeys or fixing conflicts and broken non-US layouts.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - desktop
  - keyboard
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: desktop-keyboard-shortcuts
  official: true
  domain: frontend
  security_flags: []
---

# Desktop Keyboard Shortcuts

## When to use
An app needs a shortcut system, or keys fire while typing, clash with the OS or fail on other keyboards.

## Steps
1. `grep` all current key handlers and menu accelerators into one table: action, keys, scope, platform.
2. Keep platform standards for copy, paste, undo, save, find, close and quit. Map Command on macOS where others use Control, and check redo, settings and window keys per platform.
3. Define scopes (global, window, view, text field, dialog) and precedence; the innermost handles first.
4. Put commands in one registry that feeds handlers, menus, tooltips and the help list, so displayed keys cannot drift.
5. Do not take single-letter shortcuts while text input has focus. Provide a way to turn off or remap character-only shortcuts.
6. Decide per binding between the produced character (`KeyboardEvent.key`) for mnemonic keys and the physical position (`code`) for spatial ones such as movement keys; display the label for the user's layout.
7. Ignore events during IME composition and handle AltGr, which may appear as Control plus Alt on Windows.
8. Use system-wide hotkeys only when essential: opt-in, configurable, with registration failure reported.
9. For user remapping, detect conflicts, allow reset and version the stored map.
10. In browsers avoid reserved combinations.

## Watch out for
- Control plus Alt shortcuts can block typing characters such as the at sign on several European layouts.
- Key repeat can run a destructive command many times; ignore repeats where needed.
- Every shortcut also needs a visible menu or button route.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The table has no unresolved conflicts per scope, typing in fields and composition is unaffected, and shown labels match the working keys on each target platform.
