---
name: game-ui-hud
version: 1.0.1
description: >
  Design a game HUD that ranks information by urgency, stays readable in busy combat and scales across screens and input devices. Use when planning or decluttering in-game UI.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - ui
  - design
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: game-ui-hud
  official: true
  domain: gaming
  security_flags: []
---

# Game Ui Hud

## When to use
Players miss vital information or the screen is crowded.

## Steps
1. List every piece of information with the decision it supports, how quickly it is needed, how often it changes and the cost of missing it.
2. Assign each a treatment: always visible, appears on change or threshold, on demand, shown in the world or on the character, or removed.
3. Place urgent information near where the eyes already are; keep stable positions for glanceable values. Set a limit on simultaneous alerts with priority, stacking and merge rules.
4. Pair color with shape, number, sound or position for health, teams and status.
5. Sketch wireframes for calm, heaviest combat, low health, dialogue and spectator or co-op states before art.
6. Test over the brightest, darkest and busiest backgrounds using outlines or backing plates.
7. Support safe areas, TV overscan settings where required, cutouts, supported aspect ratios including ultrawide, handheld sizes and viewing distance. Offer UI scale, opacity and per-element toggles.
8. For menus define initial focus, directional navigation, back behaviour, input device switching and states for empty, loading and failure.
9. Check readability with a glance test: show gameplay briefly and ask what the health, threat and objective were. Repeat in motion on target hardware.

## Watch out for
- Hiding information for immersion with no substitute or option.
- Judging legibility on a still mockup at desk distance.
- Damage numbers and effects covering enemy tells.
- Fixed pixel layouts that break with longer languages or larger scale.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
An information priority table and wireframes for the key states exist, and readability and scaling are tested on targets or listed as pending.
