---
name: game-vfx-checklist
version: 1.0.1
description: >
  Set and check visual effect rules for gameplay readability, timing, hit-area accuracy, flash safety and per-platform cost. Use when reviewing ability or environment effects that confuse players or drop frames.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - art
  - perf
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: game-vfx-checklist
  official: true
  domain: gaming
  security_flags: []
---

# Game Vfx Checklist

## When to use
Effects are being authored or reviewed.

## Steps
1. Give each effect a job (warn, confirm, show area, show state, decorate) and a priority. Decoration yields first.
2. Match gameplay: telegraph and active timing line up with the simulation, and the drawn area matches the true hit area. Check with debug shapes.
3. Keep allies, enemies, self and neutral hazards distinct by shape, motion, brightness and sound as well as color.
4. Stage the worst case, such as many players using abilities against a bright and a dark background from gameplay camera distance. Threats and characters must stay readable.
5. Set budgets from target measurements: live particles, emitters, overdraw, transparent layers, lights, distortion, texture memory and spawn cost per effect and in total.
6. Profile GPU and CPU on the weakest target. Large overlapping transparent quads and fill rate often cost more than particle count.
7. Define quality tiers, distance and off-screen culling, pooling and hard caps. Gameplay-critical shapes and timing survive every tier.
8. Check lifetime: stops on interrupt, death, pause and scene change, pooled instances reset, and loops cannot leak.
9. Limit full-screen flashes and flicker (no more than three flashes per second as a floor, with proper photosensitivity testing where needed) and provide intensity, shake and flash settings.
10. Keep a test scene and record pass or fail per effect.

## Watch out for
- An effect approved alone in an empty viewer.
- Culling by emitter origin so a large visible effect pops out.
- Lower settings that hide a hazard and give an advantage or disadvantage.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each reviewed effect has a readability, accuracy, safety and cost result on the stress scene, with over-budget and untested ones listed.
