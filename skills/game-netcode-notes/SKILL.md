---
name: game-netcode-notes
version: 1.0.1
description: >
  Choose and document a game's networking model: topology, authority, sync method, latency handling, join and disconnect rules, cheat limits and tests. Use before building or revising multiplayer networking.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - multiplayer
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: game-netcode-notes
  official: true
  domain: gaming
  security_flags: []
---

# Game Netcode Notes

## When to use
A team needs a written networking decision. This is the design record, not the prediction code itself.

## Steps
1. Gather genre, players per session, tolerable delay per action, platforms, bandwidth and hosting budget, competitive stakes and existing engine networking.
2. Compare topology (dedicated server, player host, peer to peer) on cost, fairness, trust, NAT traversal, relays and what happens when the host leaves.
3. Choose a sync method with reasons: state replication, deterministic lockstep, rollback, or turn commands. Lockstep and rollback need reproducible simulation; verify that rather than assume it.
4. List each object and event with its authority, send rate, reliability, ordering and relevance (who needs to know). Resend state that is quickly replaced differently from events that must arrive once.
5. For each player action, say what is predicted, how corrections appear, how remote objects are interpolated and whether the server rewinds for hits, with a maximum.
6. Define join in progress, reconnect, timeout, pause and version mismatch.
7. Mark trust boundaries: validate inputs, rates and movement server-side and send clients no hidden information they should not see. A player host can cheat; say so.
8. Estimate bandwidth per player and server at maximum load, labelled as estimate.
9. Set a test matrix of latency, jitter, loss, reordering and mixed connections using engine tools or a network shaper, with pass criteria.

## Watch out for
- Testing only on localhost or a LAN.
- Adding multiplayer after building single-player systems around immediate local state.
- Generous lag compensation that lets high-latency players hit people already behind cover.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The notes record topology, sync model, authority table, latency and disconnect rules, trade-offs rejected and a test matrix, with unmeasured figures marked.
