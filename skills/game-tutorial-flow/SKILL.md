---
name: game-tutorial-flow
version: 1.0.1
description: >
  Design a game tutorial that teaches each verb in context, checks the player can do it unaided, and allows skipping and replay. Use when new players get lost or quit early.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - ux
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
  library_id: game-tutorial-flow
  official: true
  domain: gaming
  security_flags: []
---

# Game Tutorial Flow

## When to use
The first minutes of a game need to teach without lecturing.

## Steps
1. List everything the player must know to enjoy the core loop. Cut or defer what is not needed yet, aiming for only a few early verbs.
2. Order by dependency and introduce one new idea at a time, just before its first use.
3. For each, design: a safe situation that requires the action, a short prompt, feedback, practice, then an unprompted test under light pressure and later reuse combined with others.
4. Teach through level layout and consequences first, text second. Prompts wait for the action, show current bindings for the active device and can be reread.
5. Add stepped help on observed struggle: a clearer cue, then explicit instruction, then a way past.
6. Detect players who already know a step, and never block because they did it early or differently.
7. Offer skip, replay and a help reference. Skipping must grant the same items, flags and unlocks.
8. Handle failure, reload, quit midway, rebinding, a returning player after a long break, and sequence breaks that could soft-lock.
9. Script the first ten minutes with time, player action, lesson and exit condition.
10. Watch first-time players without helping, record hesitation and wrong guesses, and log step start, completion, skip and quit.

## Watch out for
- Treating a completed prompt as learned; check later unaided use.
- Long unskippable intro before the player touches anything.
- Accessibility and control settings reachable only after the tutorial.
- Retesting only with people who have seen it before.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each core verb has introduction, practice and unaided check, skip leaves a valid state, and fresh-player observations are recorded or still pending.
