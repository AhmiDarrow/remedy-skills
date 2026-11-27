---
name: level-design-brief
version: 1.0.1
description: >
  Write a level design brief covering the teaching goal, layout, pacing, encounters and greybox pass criteria. Use before building or reworking a game level, map or mission space.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - level-design
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: level-design-brief
  official: true
  domain: gaming
  security_flags: []
---

# Level Design Brief

## When to use
A level needs to be agreed before anyone builds geometry, or a built level plays badly and has no written intent to test against.

## Steps
1. Read the design docs and one existing level. Record the player's verbs and movement metrics: walk and sprint speed, jump height and gap, cover height, minimum corridor width, camera clearance. If they are not final, say which dimensions depend on them.
2. State the level's job in one sentence: the skill taught or tested, the story change, and what the player already knows on entry.
3. Plan each new mechanic as a sequence: safe introduction, use under light pressure, twist, combination with an older skill.
4. Draw the critical path as a node graph (text or Mermaid). Mark entrances, exits, locks and keys, one-way drops, shortcuts, optional branches and checkpoints.
5. Lay the beats on a timeline with target minutes and intensity from 1 to 5, placing a quiet beat after each peak. Estimate first-time and replay duration separately.
6. Give each encounter a row: purpose, enemies or puzzle parts, space needed, ways to approach it, what the player can see before committing, retry point.
7. Plan wayfinding: the landmark visible from each major junction, how light, shape or motion pulls the eye, and what tells the player a branch is optional.
8. Set the secrets and reward count, and the hint that makes each secret findable.
9. Write greybox pass criteria that a playtest can check, such as "new players reach the second area without prompting" or "death to retry is under the project's limit".

## Watch out for
- Metrics changing after greybox, which silently breaks jumps and cover.
- Soft locks: a consumable key, a door closing behind a missing item, or a checkpoint saved after the point of no return.
- Teaching a mechanic during a fight, where the prompt gets ignored.
- A brief that describes mood and scenery but nothing a tester could fail.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The brief has the node graph, timed beats, encounter rows and checkable greybox criteria, every lock has a reachable key, and unconfirmed metrics are listed.
