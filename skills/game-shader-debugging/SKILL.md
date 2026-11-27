---
name: game-shader-debugging
version: 1.0.0
description: >
  Debug shaders that render black, pink, flickering or differently across GPUs and platforms. Use when a custom material or post effect looks wrong or fails to compile on a target.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - shaders
  - graphics
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-shader-debugging
  official: true
  domain: gaming
  security_flags: []
---

# Game Shader Debugging

## When to use
A visual bug involves a shader or its inputs.
## Steps
1. Record GPU, driver, graphics API and engine render pipeline for working and failing cases. Read the compile log; a fallback material usually means compile failure or a pipeline mismatch.
2. Capture a frame with a graphics debugger such as RenderDoc or the platform's tool. Confirm the draw happens and inspect bound resources, constants and render state.
3. Check state before shader math: culling, depth test and write, blending, scissor, target format.
4. Output intermediate values as color, one at a time: UVs, normals remapped to 0-1, masks. Flag NaN or negative values with a distinct color.
5. Guard risky math: zero-vector normalize, division by near zero, square root of negatives and `pow` with a negative base.
6. Verify space consistency: each vector in an operation must be in the same space, and normals need the proper normal transform under non-uniform scale.
7. Check color handling: color textures sampled as sRGB, data maps such as normals and roughness as linear, and conversion applied only once.
8. For cross-platform differences, check uniform buffer layout, precision qualifiers, clip space depth range, texture origin and derivatives or implicit LOD inside branches.
9. Check uninitialized outputs and varyings.
10. Retest on the failing device.
## Watch out for
- A single NaN can spread through bloom or temporal passes into large black blocks.
- Desktop GPUs often forgive precision that mobile GPUs do not.
- Unbounded shader loops can hang the GPU and reset the driver.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The bad value or state is identified in a capture, and the corrected result is verified on each target available, with untested ones named.
