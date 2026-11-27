---
name: game-dialogue-pass
version: 1.0.1
description: >
  Write or revise game dialogue for distinct voices, branching logic, line budgets, interruptions, localization and recording notes. Use when scripts feel flat, too long or break across story branches.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - narrative
  - writing
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
  library_id: game-dialogue-pass
  official: true
  domain: gaming
  security_flags: []
---

# Game Dialogue Pass

## When to use
Barks, conversations or cutscene lines need writing or editing.

## Steps
1. Read the narrative bible, character samples and script format. Note each speaker's goal, knowledge at this point, vocabulary and verbal limits.
2. Preserve line ids, variables, tags and conditions. Changing an id can break audio, translations and save data.
3. Map branches: entry conditions, flags set and read, and exits. Check each path so nobody mentions an event that has not happened, and repeat visits have their own lines.
4. For each scene state what changes. Cut lines that repeat what the player just saw; let intent show through what characters avoid or choose.
5. Make choices honest: the option text should match the tone and action of the spoken reply.
6. Apply budgets for subtitle width, reading time, choice buttons and speech length. Put gameplay-critical facts also in a log or objective, since barks get missed.
7. For repeatable barks, write enough variants, add cooldown and priority notes, and keep them short enough to interrupt.
8. Prepare for localization: whole sentences, no assembled grammar around names or counts, notes on speaker, listener, gender and wordplay.
9. Keep voice direction, context and pronunciation in separate fields from spoken text. Flag lines already recorded, since edits cost pickups.
10. Read aloud or run the script validator, and report changed ids.

## Watch out for
- Every character sharing the writer's jokes and rhythm.
- Exposition between people who both already know it.
- A variable whose longest value overflows the box.
- Imitating a real actor or living author's recognisable voice.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Branches have no unreachable or contradictory lines, budgets are met or flagged, ids and tags are intact, and changed recorded lines are listed.
