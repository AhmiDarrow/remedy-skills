---
name: game-audio-direction
version: 1.0.1
description: >
  Write game audio direction covering mood per state, adaptive music, sound categories, mix priorities, naming and implementation checks. Use when briefing composers or sound designers or fixing a messy mix.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - audio
  - design
kind: native
status: discovered
tools:
  - read
  - write
  - glob
metadata:
  source: library
  library_id: game-audio-direction
  official: true
  domain: gaming
  security_flags: []
---

# Game Audio Direction

## When to use
A game needs a shared plan for how it should sound and how sounds get into the build.

## Steps
1. Read the design pillars. For each area and game state, write the intended feeling and what the player must learn from sound alone.
2. Map music states and transitions: trigger, layers or segments, sync point (beat, bar, immediate), fade, cooldown against rapid combat toggling, and what silence is for.
3. List sound categories (dialogue, interface, player, enemy, weapons, foley, ambience, stingers). Per important event give priority, variation count, pitch or volume randomisation and spatial or flat playback.
4. Set the mix hierarchy: which cues must never be masked, what ducks what and by how much, voice limits per category and which voices are stolen first.
5. Define game parameters feeding audio (health, speed, threat, indoor) with ranges, in terms the project's engine or middleware supports.
6. Set delivery specs: format, sample rate, loop points, channel layout, naming and folders, compression and streaming versus memory per platform, and a memory budget.
7. Choose a measured loudness target and true peak ceiling after checking current platform requirements, and test on headphones, TV and small speakers.
8. Require sliders per category, subtitles and captions, mono option and visual backups for critical cues. Record the license for every outside asset.
9. Write a test list: missing or doubled events, loops that never stop, pause and scene changes, focus loss, many simultaneous sources.

## Watch out for
- A frequently heard sound with one variation becomes irritating fast.
- Mixing only on studio monitors with one category playing.
- Reference tracks used as "make it sound exactly like this" invite copying.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A writer or composer and an implementer can each work from the document: states, events, priorities, specs and test list are filled in, with undecided values marked.
