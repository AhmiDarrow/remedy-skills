---
name: multiplayer-session-design
version: 1.0.1
description: >
  Design a multiplayer session lifecycle from party and matchmaking through play, disconnects, reconnects and results. Use when planning lobbies, drop-in play or handling players leaving mid-match.
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
metadata:
  source: library
  library_id: multiplayer-session-design
  official: true
  domain: gaming
  security_flags: []
---

# Multiplayer Session Design

## When to use
A game needs rules for how players get into a session, stay in it and leave it. Movement prediction and replication detail are a separate netcode task.

## Steps
1. Fix the facts: players per session, teams, match length, live or asynchronous, ranked or casual, platforms and cross-play.
2. Choose hosting and authority: dedicated server, player host or peer-to-peer. State who decides outcomes and who writes rewards.
3. Draw a state machine: party, queued, match found, connecting, loading, ready check, playing, results, rematch or exit. Give every waiting state a timeout and a destination on failure.
4. Define party rules: leader powers, invite expiry, join in progress, size and skill limits, full or closed sessions, version mismatch, blocked players meeting.
5. Set matchmaking constraints (region, latency, mode, skill) and how each widens with wait time, including what never widens. Handle small populations.
6. Write a table for each interruption: quit, crash, network drop, app suspended, server loss. Specify grace period, what the character does meanwhile, reconnect identity, backfill, and effect on rank and rewards.
7. With a player host, choose between ending the match and migrating. Migration needs a successor rule, sufficient state on the successor, and handling of a bad-faith host.
8. Make result submission safe to repeat using a match id, and define what happens if the match never reports.
9. Add mute, block, report and vote-kick with abuse limits.
10. List test cases for each transition, including two players leaving at once and a drop during results.

## Watch out for
- A leaver penalty that also punishes server faults.
- Rejoin creating a second copy of the player or granting rewards twice.
- Trusting a client or player host for ranked results.
- Cancel and match-found arriving at the same moment with no rule for which wins.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every state has exits for success, timeout and disconnect, rewards cannot be granted twice, and each interruption has a written outcome and a test case.
