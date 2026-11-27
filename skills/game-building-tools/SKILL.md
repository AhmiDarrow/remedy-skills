---
name: game-building-tools
version: 1.0.1
description: >
  Design an in-game building system with placement rules, snapping, clear rejection reasons, budgets, saved layouts and multiplayer permissions. Use when players will construct bases, levels or objects.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - systems
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: game-building-tools
  official: true
  domain: gaming
  security_flags: []
---

# Game Building Tools

## When to use
Players place, edit and share structures inside a game.

## Steps
1. State what players build and why, and the platforms and inputs. Precision with a gamepad or touch changes the whole tool.
2. Define the spatial model: grid, sockets, free placement or a mix, with rotation steps, snap priority and a way to override snapping.
3. Specify each piece as data: id, footprint, sockets, cost, support, collision and allowed surfaces.
4. List validity rules (overlap, terrain, support, protected zones, resources, limits). Show a ghost preview with a specific reason on rejection, using more than red and green.
5. Decide what happens when support is removed: block it, cascade collapse with a preview, or allow floating. Test cycles that support each other with no ground contact.
6. Prevent traps: blocked spawns, doors, quest paths and sealing in other players, with an unstick route.
7. Add undo, redo, move, copy and area delete, with defined refunds that cannot create resources.
8. Set budgets from measured cost on the weakest device (pieces, lights, physics bodies, simulated parts) and show usage before the limit.
9. In multiplayer, the server validates every placement and permission; resolve simultaneous edits, rate-limit, log destructive actions and allow rollback of griefing.
10. Save layouts with schema version and stable piece ids, handle removed or unowned pieces, and treat shared blueprints as untrusted input with size limits, reporting and moderation.

## Watch out for
- Checking validity only in the preview, while state changed before confirmation.
- Demolish-and-replace loops that duplicate materials.
- Navigation and physics rebuilt fully on every single placement.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Placement, removal, refund, permission, budget and save rules are written with their edge cases, and a stress and abuse test list exists.
