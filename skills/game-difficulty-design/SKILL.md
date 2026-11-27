---
name: game-difficulty-design
version: 1.0.1
description: >
  Design difficulty settings and assists by choosing which skills each changes, with per-level values and tests for every mode. Use when adding difficulty options or when a game is too hard or too flat.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - design
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: game-difficulty-design
  official: true
  domain: gaming
  security_flags: []
---

# Game Difficulty Design

## When to use
Players of different skill need a game that stays recognisably itself.

## Steps
1. List the demands the game makes: reaction, precision, planning, resource management, knowledge, endurance. Mark which are the intended experience.
2. Define each preset by the player it serves and what they should feel, not only as a percentage.
3. Map parameters to demands: wind-up and parry windows, enemy count and attack tokens, aggression, accuracy, resources, checkpoint spacing, hints, puzzle help. Health and damage are two levers, not the whole design.
4. Tabulate values per preset in data, check time-to-kill and hits-to-die at each progression stage, and watch for combinations that stack.
5. Offer granular assists apart from presets (game speed, aim, timing, damage taken) with plain descriptions.
6. Let players change settings mid-game. Say what changes immediately, and how saves, achievements, leaderboards and multiplayer treat it.
7. If difficulty adapts automatically, define signals, limits, smoothing and recovery; avoid visible swings and tell players or give an off switch. Never adapt competitive matches or tie it to spending.
8. Test each preset with matching players: deaths by cause, retries, completion time, quit points, resource starvation.

## Watch out for
- Hard mode that is only longer fights.
- Easy mode that skips the lesson later content requires.
- A choice at first launch with no information and no way back.
- Adaptive systems players exploit by failing on purpose.
- Labels or messages that mock the easier choice.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each preset and assist has stated values, effects and change rules, and has playtest results or is marked untested.
