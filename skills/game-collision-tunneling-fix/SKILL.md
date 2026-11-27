---
name: game-collision-tunneling-fix
version: 1.0.0
description: >
  Fix fast objects passing through walls, floor snagging and jittery contacts in 2D or 3D games. Use when bullets skip targets or characters clip, stick or bounce on level geometry.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - physics
  - collision
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-collision-tunneling-fix
  official: true
  domain: gaming
  security_flags: []
---

# Game Collision Tunneling Fix

## When to use
Collision results are wrong at high speed, thin geometry or tile seams.
## Steps
1. Build a repeatable test scene with the failing speed, angle and geometry, plus a debug draw of shapes, sweeps and contact normals.
2. Compare movement per physics step with obstacle thickness plus object size. If movement is larger, discrete overlap can miss it.
3. Check how the object moves. Setting the transform position directly bypasses sweeping; use the engine's velocity, move-and-collide or cast API.
4. For projectiles, cast a ray or shape from previous to next position each step, with correct handling of the starting overlap and self-collision filter.
5. For dynamic bodies, enable continuous collision detection on the specific fast ones; check which pairs the engine's modes cover.
6. For custom kinematic movement, sweep to first impact, keep a small skin distance, remove velocity into the normal and continue with the remainder for a limited number of iterations.
7. In tile worlds, resolve axes separately or sweep through crossed cells; merge adjacent colliders or use edge-aware shapes to stop seam snagging.
8. Treat ground detection with a short cast and slope limit rather than a single contact flag.
9. Test at extreme speed, low tick rate, corners and moving platforms.
## Watch out for
- Thickening walls or capping speed may hide the bug until a new level or powerup.
- Raising the physics rate costs CPU everywhere.
- Non-uniformly scaled or concave mesh colliders can behave unexpectedly.
- Fast moving obstacles need relative motion considered, not only the projectile's.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The test scene passes at above the maximum game speed over many randomized starts with no pass-through or stuck state.
