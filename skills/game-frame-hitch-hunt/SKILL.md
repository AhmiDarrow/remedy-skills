---
name: game-frame-hitch-hunt
version: 1.0.0
description: >
  Find the cause of intermittent frame spikes and stutter in a game, such as GC, asset loads or shader compilation. Use when average FPS is fine but play still hitches.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - profiling
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-frame-hitch-hunt
  official: true
  domain: gaming
  security_flags: []
---

# Game Frame Hitch Hunt

## When to use
Stutter is periodic or tied to events. This is about spikes, not a steadily low frame rate.
## Steps
1. Log per-frame times in a release-like build on target hardware, with event markers (spawn, area entry, effect first use, autosave). Use 99th percentile and worst frame, not mean FPS.
2. Classify by pattern: regular intervals suggest garbage collection or timers; first-time-only suggests shader or pipeline compilation and lazy loading; crossing boundaries suggests streaming.
3. Capture a spike with the engine profiler or a frame profiler, using a trigger that saves frames above the budget.
4. Determine whether the main thread, render thread or GPU was late. A main thread waiting on the GPU or vsync is not the culprit.
5. For GC, find per-frame allocations: temporary collections, string building, closures and boxing. Remove them from the loop.
6. For loading, move disk reads and decompression off the main thread and budget main-thread activation across frames; preload what is predictably needed.
7. For shader compilation, collect and prewarm the variants used, following the engine and graphics API's method.
8. For bursts of spawns or AI updates, spread work over frames with a per-frame budget.
9. Replay the same route and compare frame time traces.
## Watch out for
- Editor and debug builds create spikes that players never see.
- A second run uses warm shader and file caches; clear them to retest first-time hitches.
- Logging every frame to disk synchronously creates its own hitch; buffer it.
- Uneven frame pacing can stutter with no long CPU frame; check present timing.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The spike is reproduced, attributed to a profiled cause, and the same route shows the worst frames within the agreed budget.
