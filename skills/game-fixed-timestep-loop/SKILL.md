---
name: game-fixed-timestep-loop
version: 1.0.0
description: >
  Implement a fixed-timestep game loop with interpolation so physics and gameplay behave the same at any frame rate. Use when speed, jumps or collisions change with FPS.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - physics
  - simulation
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-fixed-timestep-loop
  official: true
  domain: gaming
  security_flags: []
---

# Game Fixed Timestep Loop

## When to use
Game logic runs on variable frame time, or motion stutters despite a good frame rate. If an engine already has a fixed update, use it.
## Steps
1. Find where simulation, input and rendering happen and every use of delta time.
2. Move physics and gameplay rules into a step with constant `dt`, keeping rendering per frame.
3. Use an accumulator: add measured frame time from a monotonic clock, and run steps while it holds at least one `dt`.
4. Clamp the incoming frame time and limit steps per frame, so a breakpoint or hitch cannot cause a spiral of ever more catch-up work. Decide that excess time is dropped.
5. Keep previous and current transforms and render at `alpha = accumulator / dt` between them. Interpolate rotations on the shortest arc.
6. Snap both states on teleport or spawn so objects do not streak across the screen.
7. Latch button presses until a simulation step consumes them; a frame with zero steps must not lose a press, and one with several must not fire it twice. Apply mouse deltas once.
8. Apply per-frame damping such as `v *= 0.9` as a rate inside the fixed step.
9. Test with the frame rate capped at several very different values and with injected stalls; compare jump height and travel distance over equal simulated time.
## Watch out for
- Moving rendered objects directly while physics also moves them causes jitter.
- Cameras updated on a different clock from their target stutter.
- Interpolation shows state up to one step behind; account for it in feel and hit feedback.
- Previously tuned constants will need retuning after the change.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Recorded distances and jump arcs agree across the tested frame rates, and no input is dropped or doubled.
