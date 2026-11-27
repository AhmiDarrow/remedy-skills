---
name: game-perf-budget
version: 1.0.1
description: >
  Set per-platform budgets for frame time, memory, loading, hitches and content, with a repeatable capture method and owners. Use when starting production or when performance keeps slipping.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - perf
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: game-perf-budget
  official: true
  domain: gaming
  security_flags: []
---

# Game Perf Budget

## When to use
A team needs limits that content and code can be checked against.

## Steps
1. Fix target and minimum devices, resolution, quality preset and frame rate. Frame time is 33.3 ms at 30 FPS, 16.7 ms at 60 and 8.3 ms at 120.
2. Capture worst realistic scenes on the weakest target in a release-like build. Record main thread, render thread and GPU times separately; they run in parallel, so do not simply add them.
3. Leave headroom for operating system, spikes and thermal throttling, then split CPU and GPU time between systems with owners.
4. Budget memory from the platform's usable limit, not installed RAM: textures, meshes, audio, code and heap, render targets, streaming pool, plus reserve and transition peaks.
5. Define hitches (frames over a stated threshold), percentiles such as 95th and 99th, load times, install and patch size, and for mobile, sustained heat and battery.
6. Derive content limits (triangles, draw calls, texture sizes, lights, particles, bones) from measurements in this game, as guides with an exception process.
7. Create fixed benchmark routes with build, device and settings recorded; compare several runs and note the noise.
8. Automate what is stable (asset size checks, memory, benchmark route) with warn and fail thresholds, and name who acts on a failure.

## Watch out for
- Average FPS hides stutter.
- Measuring in the editor or on a developer's high-end machine.
- A short run that never reaches thermal throttling or leak growth.
- Copying another game's draw-call limits.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each target has numeric budgets with current measurements or "not yet measured", a repeatable capture route, owners and a response to overruns.
