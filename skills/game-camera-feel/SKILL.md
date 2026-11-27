---
name: game-camera-feel
version: 1.0.1
description: >
  Tune a game camera's follow, look, collision, framing and combat behaviour, with comfort options and repeatable tests. Use when a camera lags, jitters, clips, hides threats or causes nausea.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - feel
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
  library_id: game-camera-feel
  official: true
  domain: gaming
  security_flags: []
---

# Game Camera Feel

## When to use
The camera gets in the way of play.

## Steps
1. Identify camera type and modes (explore, combat, aim, vehicle, interior) and where each is set. Reproduce each complaint with place and action.
2. Check update order before tuning: the camera should move after the target's interpolated position is final. Mixing physics-step and render-frame updates causes jitter that smoothing only hides.
3. Make smoothing frame-rate independent, such as a factor of `1 - exp(-rate * dt)` or a damped spring, not a fixed lerp per frame.
4. Tune follow separately per axis: dead zone, look-ahead, and vertical behaviour so jumps do not bob the view.
5. Keep player-driven look direct. Mouse delta is not multiplied by frame time; stick input is a rate, so it is. Expose dead zone and response curve.
6. For collision, cast a volume rather than a thin ray, pull in quickly, ease out slowly, ignore thin props, and fade geometry or the character when very close.
7. Define combat framing, lock-on selection and switching, off-screen threat indicators and blends between modes; never snap away control without reason.
8. Offer sensitivity per axis, invert per axis, field of view where the view allows, and shake, bob, motion blur and auto-rotate settings that can reach zero.
9. Record a fixed test route (narrow corridor, corner, ledge, large enemy, crowd, fast fall) and compare changes at low and high frame rates.

## Watch out for
- Extra lag added for a cinematic look reads as input delay.
- Auto-rotation fighting the player's stick.
- Judging comfort only from people who built the game and are used to it.
- Aim assist hidden inside camera code, where it affects menus or other modes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The test route plays without the reported faults at the target frame rates, changed values are recorded with reasons, and comfort options work or are listed as gaps.
