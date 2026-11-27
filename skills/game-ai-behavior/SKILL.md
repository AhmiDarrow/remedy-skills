---
name: game-ai-behavior
version: 1.0.1
description: >
  Design enemy or NPC behaviour with perception, memory, decision logic, group rules, difficulty settings and debug views. Use when enemies feel dumb, unfair, erratic or all act alike.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - ai
  - systems
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
  library_id: game-ai-behavior
  official: true
  domain: gaming
  security_flags: []
---

# Game Ai Behavior

## When to use
Characters need believable, readable decisions. Route finding itself is a separate problem.

## Steps
1. Define each role by what it forces the player to do (rusher forces movement, sniper forces cover). Read existing behaviour code and the engine's tools first.
2. Pick the simplest model that fits: finite state machine for a few clear states, behaviour tree for layered priorities, utility scoring for many competing choices, planning only if action chains must vary.
3. Specify perception: view range and angle, line-of-sight checks, hearing events, time to notice, and what is remembered (last known position, age) and when forgotten. Decisions use this memory, not the player's true position.
4. Write a transition table: from, trigger, to, interrupt priority, minimum duration and exit if the goal becomes impossible. Cover idle, suspicious, search, engage, retreat, stunned and death.
5. Add hysteresis, cooldowns or score margins so characters do not flicker between two choices.
6. Coordinate groups with attack tokens, claimed cover and spacing so they neither all strike at once nor queue politely.
7. Make intent readable through animation, barks and pauses.
8. Scale difficulty by reaction time, accuracy, aggression, group tokens and tactics, listing values per level.
9. Provide debug overlays for state, target, perception shapes, scores and the reason for the last switch, plus a test scene per behaviour.
10. Set update rates and stagger expensive queries across frames.

## Watch out for
- Omniscience, such as turning toward a hidden player, destroys trust.
- No fallback when a target, path or cover disappears leaves characters frozen.
- Exploits at doorways, ledges and leash limits.
- Unseeded randomness makes bugs unreproducible.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each role has a transition or scoring table, perception values, failure fallbacks and difficulty values, and the test scenes show the intended behaviour or are listed as unrun.
