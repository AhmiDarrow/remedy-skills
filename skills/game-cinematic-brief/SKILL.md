---
name: game-cinematic-brief
version: 1.0.1
description: >
  Brief an in-game or pre-rendered cutscene with story purpose, timed shots, audio, gameplay state handoff and safe skipping. Use when commissioning or planning a game cinematic.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - cinematic
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: game-cinematic-brief
  official: true
  domain: gaming
  security_flags: []
---

# Game Cinematic Brief

## When to use
A game scene needs a brief that animation, audio and gameplay can all work from.

## Steps
1. State what the player must understand or feel afterwards and why this cannot be played instead. Set maximum length.
2. Choose in-engine or pre-rendered and note consequences: player customisation, time of day, localisation, file size.
3. Record the state before: location, who is alive, equipped gear, choices made, camera position. List each branch variant.
4. Write timed beats: shot, framing, camera move, action, dialogue, sound, and the one thing the eye should follow. Total the durations and read dialogue aloud against them.
5. Define the exit state: positions, inventory, quest flags, enemies, music and camera, and how control returns. Give the player a safe moment before danger.
6. Specify pause and skip. Skipping must apply the same exit state as watching, from any moment; protect against accidental skips and allow replay if the game supports it.
7. List what it needs: rigs, animations, effects, voice, music, facial work, streaming and load points, with owners and reusable assets.
8. Include subtitles, safe framing for supported aspect ratios, reduced flashing, and timing room for longer dubbed languages.
9. Set first-cut acceptance with a rough previz: story reads without final art, length fits, handoff works.

## Watch out for
- Rewards or flags granted by timeline events that never fire when skipped.
- An unskippable scene between a checkpoint and a hard fight.
- Custom outfits or companions replaced by defaults.
- Cameras clipping because the player arrived from an unplanned position.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The brief has purpose, timed beats, entry and exit state, skip behaviour, asset owners and first-cut criteria.
