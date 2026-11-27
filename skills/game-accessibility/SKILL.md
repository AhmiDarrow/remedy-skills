---
name: game-accessibility
version: 1.0.1
description: >
  Audit a game for visual, hearing, motor and cognitive barriers and plan options that remove them, starting with the core loop. Use when adding accessibility to a design or build.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - a11y
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: game-accessibility
  official: true
  domain: gaming
  security_flags: []
---

# Game Accessibility

## When to use
A game in design or production should be playable by more people.

## Steps
1. Walk from first boot to a completed core loop. At each step list what the player must see, hear, press, time, remember and read.
2. Mark every single-channel or single-ability demand as a barrier with where it occurs.
3. Vision: scalable UI and subtitles, contrast, backgrounds behind text, shapes or patterns beside color, customisable key colors, and sound or narration for critical visual cues. A colorblind screen filter alone rarely fixes meaning.
4. Hearing: subtitles with speaker names, captions for meaningful sounds with direction, visual cues for audio warnings, and separate volume sliders.
5. Motor: full remapping on every device, hold or toggle alternatives, no forced rapid tapping or simultaneous presses, adjustable sensitivity, dead zones and timing windows.
6. Cognitive: pause anywhere possible, objective recap, replayable tutorials, text that waits for the player, and difficulty assists adjustable separately and mid-game.
7. Comfort and safety: reduce shake, motion blur and flashing. Flashing content needs removal or testing; a warning screen is not a fix.
8. Make options reachable before the first demanding or flashing content, with menus usable themselves (narration or platform screen reader support where available). Save them per profile.
9. Rank by whether the barrier blocks play, how many it affects and cost. Test with disabled players, and check current platform and legal requirements, such as for voice and text chat.

## Watch out for
- Describing assists as cheating or locking achievements without saying so beforehand.
- Remapping that leaves on-screen prompts showing old buttons.
- Claiming a feature in store tags that works only in parts of the game.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each barrier in the core loop has an option, a decision with owner, or an explicit open gap, and tested features are separated from planned ones.
