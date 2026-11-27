---
name: game-pathfinding-implementation
version: 1.0.0
description: >
  Implement or fix grid and navmesh pathfinding that is correct, smooth and within frame budget. Use when NPCs take odd routes, cut corners, jam together or stall the game.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - pathfinding
  - ai
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-pathfinding-implementation
  official: true
  domain: gaming
  security_flags: []
---

# Game Pathfinding Implementation

## When to use
Agents need to navigate a world. Behavior choice is a different problem; this covers getting from here to there.
## Steps
1. Describe the world: static or changing, grid or free space, agent sizes, movement costs and agent count. Prefer the engine's navigation system if it covers these.
2. For grids use A* with a binary heap; for many agents sharing a goal use a single flow field or Dijkstra from the goal.
3. Match the heuristic to movement: Manhattan for four directions, octile for eight with diagonal cost, Euclidean for any angle. Overestimating trades optimality for speed, so do it knowingly.
4. Block diagonal moves that squeeze between obstacles or clip corners, and account for agent radius by inflating obstacles or per-size navigation data.
5. Handle unreachable goals early with connectivity regions, and return a best partial path under a node limit.
6. Smooth using line-of-clearance checks with agent width, or a funnel algorithm on navmeshes.
7. Queue requests with a per-frame budget; slice long searches or run them on a snapshot off the main thread.
8. Invalidate paths only when changes touch them, and stagger replanning.
9. Add separate local avoidance and stuck detection based on progress over time.
10. Test against brute-force shortest costs on small random maps, plus maze, sealed goal and crowd cases.
## Watch out for
- Replanning every agent every frame is the usual performance failure.
- Mismatch between navigation data and collision geometry makes agents walk into walls.
- Ties produce zigzags; use a consistent tie breaker.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Costs match the reference on test maps, unreachable cases terminate within budget, and the crowd scene stays within frame time.
