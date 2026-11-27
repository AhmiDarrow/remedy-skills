---
name: game-large-world-precision
version: 1.0.0
description: >
  Fix jitter, physics errors and timer drift caused by floating point precision far from the origin or in long sessions. Use when meshes shake in distant areas or after long uptime.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - math
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-large-world-precision
  official: true
  domain: gaming
  security_flags: []
---

# Game Large World Precision

## When to use
Artifacts grow with distance from world origin or with time since launch.
## Steps
1. Confirm the pattern: run the same scene near the origin and far away, or set the game clock to a large value.
2. Calculate spacing between adjacent 32-bit floats at that magnitude and the unit scale; compare it with the movement or detail that breaks.
3. Locate where precision is lost: simulation positions, physics, animation, vertex transforms, shader time or accumulated timers.
4. For time, keep an integer tick count or double, and send shaders a wrapped time whose period matches the effects' cycles.
5. For rendering, use camera-relative transforms computed in higher precision before converting to floats.
6. For simulation, choose among engine large-world support, origin rebasing, or sector coordinates plus local offsets. Check engine documentation first.
7. If rebasing, shift everything holding world positions in one step: bodies, particles, trails, navigation, audio, cached targets and previous-frame interpolation data.
8. Keep saves and network messages in stable global coordinates, converted at the boundary.
9. For depth flicker, treat separately: raise the near plane and consider reversed Z with a floating depth buffer.
10. Test across a rebase boundary while moving fast.
## Watch out for
- Shrinking the world scale alone does not increase relative precision.
- World-space texture and noise shaders jump on rebase unless offset.
- Multiplayer peers may use different local origins, so never exchange local positions.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The scene at maximum distance and long uptime is visually and physically indistinguishable from near origin within the stated tolerance.
