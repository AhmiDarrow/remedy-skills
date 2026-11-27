---
name: game-draw-call-batching
version: 1.0.0
description: >
  Reduce rendering CPU cost from too many draw calls using batching, instancing, atlases and culling, guided by captures. Use when a game is render-thread bound in busy scenes.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - rendering
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
  library_id: game-draw-call-batching
  official: true
  domain: gaming
  security_flags: []
---

# Game Draw Call Batching

## When to use
Profiling shows time in draw submission rather than gameplay code or pixel shading.
## Steps
1. Prove the bottleneck: lower the render resolution. If frame time falls greatly, you are likely GPU fill or shading bound and batching will not help much.
2. Capture the worst scene and record draws, state changes, triangles, shadow passes and render thread time.
3. Find why consecutive draws split: different material or shader variant, texture, blend mode, mesh, lighting data or sort order. Use the engine's frame debugger to show the break reason.
4. For repeated identical meshes use GPU instancing with per-instance data, avoiding per-object material clones.
5. For sprites and UI, atlas textures with padding against bleeding, and separate frequently changing UI from static parts.
6. For static geometry, merge by material within spatial chunks so culling still works.
7. Check culling and level of detail: off-screen objects, distant small objects and shadow casters.
8. Reduce multiplied passes: shadow cascades, extra cameras and per-light passes.
9. Apply one technique at a time and recapture the same view.
## Watch out for
- Merging a whole level into one mesh draws everything all the time and raises memory.
- Static batching can duplicate vertex data heavily.
- Transparent objects must keep back-to-front order, which limits batching.
- Fewer draws is not the goal if frame time on target hardware does not improve.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The same capture shows lower render thread and frame time on target hardware, with visuals checked for sorting, bleeding and culling errors.
