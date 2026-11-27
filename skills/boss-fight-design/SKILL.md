---
name: boss-fight-design
version: 1.0.1
description: >
  Design a boss encounter with phases, readable tells, fair counterplay, failure recovery, assist options and a tuning plan. Use when creating or fixing a boss that feels unfair, dull or spongy.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - combat
  - design
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: boss-fight-design
  official: true
  domain: gaming
  security_flags: []
---

# Boss Fight Design

## When to use
A game needs a boss, or an existing one frustrates or bores testers.

## Steps
1. Read the player's verbs and stats at this point in the game. State the boss's role: skill exam, new twist or story peak. It may only demand abilities already taught or taught safely within the fight.
2. Set target fight length, expected attempts and the main lesson.
3. Define each attack as a table row: tell (pose, sound, effect), wind-up time, active window, range, damage, correct responses and recovery opening.
4. Give each phase a trigger (health, time, objective), one new idea and a recombination of old ones. Say what happens if burst damage crosses a threshold mid-attack or skips a phase.
5. Write selection rules: cooldowns, range conditions, forbidden back-to-back pairs and a guaranteed opening after pressure. Check overlapping hazards always leave a reachable safe response.
6. Plan failure: checkpoint position, retry time, skipped cutscenes and whether phase progress or consumables are kept.
7. Check every build and difficulty can win, and list exploits such as safe spots, leashing and stun loops.
8. Add options: reduced flashing and shake, cues in both sight and sound, timing or damage assists.
9. Plan tuning with first-timers and veterans: attempts, death cause per attack, phase reached, time to win, quit points.

## Watch out for
- A tell hidden by the camera, particle effects or off-screen position is not a tell.
- Difficulty from more health alone only lengthens the same lesson.
- Reading the player's button presses to counter them feels like cheating.
- Testing only with the developers, who already know every pattern.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A written encounter sheet has the attack table, phase rules, edge cases, recovery, assists and playtest measures, with numbers marked as untested starting values.
