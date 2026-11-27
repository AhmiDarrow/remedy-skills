---
name: game-input-mapping
version: 1.0.1
description: >
  Define action-based input maps for keyboard, mouse, gamepad and touch with contexts, conflict rules, safe rebinding and matching prompts. Use when adding controls or remapping, or fixing input conflicts.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - input
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: game-input-mapping
  official: true
  domain: gaming
  security_flags: []
---

# Game Input Mapping

## When to use
Controls need designing, or keys clash, stick or cannot be changed.

## Steps
1. Use the engine's input action system if present. List actions by meaning (`Jump`, `Interact`), with type: button, 1D or 2D axis.
2. Group into contexts (gameplay, vehicle, menu, chat, build) with priority and whether input passes through. Typing in chat must not move the character.
3. Draft defaults per device following platform conventions for confirm and back. Bind keyboard movement by physical position so non-QWERTY layouts work, and display the user's layout's key label.
4. Define tap, hold, double-tap and chords with timings. A tap that shares a button with a hold fires late or on release; avoid that for time-critical actions.
5. Detect conflicts within contexts active together. On rebind, offer swap, replace or cancel, and never leave required actions unbound.
6. Keep a protected escape route and reset-to-default; binding capture needs cancel and timeout.
7. Offer toggle for holds, alternatives to mashing and chords, sensitivity, invert, dead zones and curves, and separate left-handed layouts.
8. Save bindings per profile with a version, keyed by action id; merge new defaults without wiping custom ones.
9. Generate prompts from current bindings and last active device, with hysteresis so stick drift does not flicker icons.
10. Test hot-plug, disconnect pause, two controllers, focus loss with keys held, and context switches mid-press.

## Watch out for
- Stuck movement after Alt-Tab because the release event never arrived.
- The press that closes a menu also triggering a gameplay action.
- Assuming every controller reports the same button names.
- Platform-reserved buttons and shortcuts used as bindings.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every required action is reachable on each supported device, rebinding survives restart, prompts match bindings, and the device test results are listed.
