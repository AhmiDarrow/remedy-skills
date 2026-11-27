---
name: game-client-prediction-reconciliation
version: 1.0.0
description: >
  Implement client-side prediction, server reconciliation and entity interpolation for a networked action game. Use when player movement feels laggy, rubber-bands or remote players jitter.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - game-programming
  - netcode
  - multiplayer
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: game-client-prediction-reconciliation
  official: true
  domain: gaming
  security_flags: []
---

# Game Client Prediction Reconciliation

## When to use
An authoritative server model exists or is chosen, and the client needs to feel responsive. Use the engine's built-in support if it already does this.
## Steps
1. Separate a movement step function of state, input and fixed delta, shared by client and server and free of rendering and audio side effects.
2. Number every input per tick. The client applies it immediately and stores it in a ring buffer.
3. The server validates and clamps inputs, rate limits them, simulates, and returns state with the last processed input number. Never accept client positions as truth.
4. On receipt, the client discards acknowledged inputs, resets to server state and replays the rest.
5. Include all state affecting movement in snapshots: velocity, grounded flag, dash cooldowns and status effects. Missing fields cause constant corrections.
6. Smooth small visual errors by decaying an offset on the rendered model while the simulated state is corrected at once; snap beyond a threshold.
7. Render remote entities slightly in the past, interpolating buffered snapshots with enough delay to cover jitter and some loss; cap extrapolation.
8. Suppress duplicate sounds and effects during replay, and reconcile predicted spawns by ID.
9. Test with injected latency, jitter, loss and reordering, and log correction size per tick.
## Watch out for
- Client and server using different tick rates or collision data will rubber-band forever.
- Redundantly send recent inputs over unreliable transport rather than stalling on one lost packet.
- Lag compensation for hits is separate and needs server limits on how far it rewinds.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Under the chosen bad-network profile local control responds immediately, corrections stay near zero without external forces, and remote motion is smooth.
