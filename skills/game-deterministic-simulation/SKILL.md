---
name: game-deterministic-simulation
version: 1.0.0
description: >
  Make game simulation reproducible from inputs and a seed for replays, lockstep or procedural worlds. Use when replays drift, peers desync or the same seed builds different maps.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - determinism
  - procgen
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-deterministic-simulation
  official: true
  domain: gaming
  security_flags: []
---

# Game Deterministic Simulation

## When to use
The same starting state and inputs must give the same result. Decide first whether that means same binary and machine, or across platforms.
## Steps
1. Run the simulation twice from one recorded input log and hash canonical state every tick. The first differing tick locates the bug.
2. Dump both states at that tick and diff by system and entity.
3. Drive simulation only by a fixed tick and recorded inputs; remove wall clock time and frame delta.
4. Replace global random calls with owned generators using a specified algorithm. Give each concern its own stream (terrain, loot, AI, visuals) so a cosmetic effect cannot shift gameplay rolls.
5. For worlds generated in chunks, derive each chunk's seed from world seed and coordinates with a stable hash, not from visit order.
6. Remove ordering dependence: unordered map iteration, pointer-address sorting, unstable sorts with ties, physics callbacks and multithreaded result order.
7. Do not use language hashes that are randomized per process.
8. For cross-platform lockstep, avoid relying on floating point matching across compilers and CPUs; use fixed point or a proven deterministic math and physics library, or choose state synchronization instead.
9. Save generator states with saves and snapshots, and version the generator algorithm so old seeds are handled knowingly.
10. Run the hash comparison automatically across all target builds.
## Watch out for
- Many engine physics systems do not promise cross-machine determinism; check the documentation.
- Uninitialized memory causes rare, unrepeatable divergence.
- Pooled objects retaining old fields break determinism.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Long input replays produce identical per-tick hashes on every configuration claimed as deterministic.
