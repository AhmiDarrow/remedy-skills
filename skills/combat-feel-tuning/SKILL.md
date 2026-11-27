---
name: combat-feel-tuning
version: 1.0.1
description: >
  Tune how combat feels by measuring input-to-response timing, then adjusting buffering, cancels, hit stop and feedback one at a time. Use when attacks feel sluggish, floaty, weak or unresponsive.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - combat
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
  library_id: combat-feel-tuning
  official: true
  domain: gaming
  security_flags: []
---

# Combat Feel Tuning

## When to use
Combat works mechanically but feels wrong.

## Steps
1. Turn the complaint into a moment: which action, from which state, expected versus actual. "Floaty" and "unresponsive" have different causes.
2. Locate where timing lives (animation events, data files, code). For each attack record startup, active and recovery, cancel windows, movement during it, hit stop, stagger and knockback, in milliseconds or in frames with the tick rate.
3. Trace input to visible response: polling, simulation step, animation blend, camera and display delay. Slow-motion video of controller and screen shows it. Check that button presses are not lost between fixed updates.
4. Check forgiveness: input buffer, cancel into dodge or block, grace timing after leaving ledges, and gentle target magnetism. Start with a buffer around 100-150 ms as a trial value, not a rule.
5. Check hit confirmation in layers: enemy reaction, impact sound, hit stop, effects, camera, vibration. Whiff, block, hit and kill must read differently.
6. Check enemy tells, hitbox against visible weapon, and invulnerability windows with debug drawing.
7. Change one variable group at a time, exposed as data for live editing. Record old value, new value, reason and result.
8. Write a five-minute test script (single enemy, crowd, interrupted combo, low health) and compare versions blind where possible.

## Watch out for
- Hiding slow startup with more shake and particles.
- Timing tied to frame rate, so feel changes between 30 and 144 FPS.
- Hit stop that also freezes input reading, or desynchronises networked play.
- Shake, flashes and vibration without an option to reduce them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each change has before and after values and a stated test result, behaviour matches across target frame rates, and unplayed changes are labelled untested.
