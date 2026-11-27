---
name: quest-design
version: 1.0.1
description: >
  Design a game quest with objectives, world-state flags, branches, failure and abandon rules and rewards. Use when writing a new mission or fixing quests that soft-lock or break out of order.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - narrative
  - design
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: quest-design
  official: true
  domain: gaming
  security_flags: []
---

# Quest Design

## When to use
A quest needs a specification that writers, scripters and testers can all work from.

## Steps
1. Search the project's quest data for the format, flag naming, and any quests sharing this one's characters, places or items.
2. State why the player cares, what changes in the world, and what the quest asks the player to do that the previous one did not.
3. Define start conditions, how the player discovers it, and what happens if they are not yet eligible.
4. Write a state table: state, objective text, completion trigger, flags set, next states. Include optional objectives and branches.
5. Walk every objective out of order: target already dead, item already held or sold, area already visited, character moved by another quest.
6. Define failure, abandon and retry: what resets, what persists, how quest items are returned or removed, and whether the player is warned before a point of no return.
7. Protect required characters and items, or give each a fallback path.
8. Check save and load mid-step, death during a scripted moment, and, in co-op, who owns progress when a player joins or leaves.
9. Set rewards against the project's economy values and ensure they are granted once only.
10. Draft short objective lines that say where to go and what to do without relying on voiced dialogue, and record string keys.
11. Convert the state table into a test list covering each branch and edge case.

## Watch out for
- Triggers that fire only on entering a volume the player is already inside.
- Counting pickup events instead of checking inventory.
- Choices presented as different that set identical flags without that being intended.
- Repeatable quests that can be farmed for unlimited rewards.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every state has a way forward or a declared failure, out-of-order cases are handled, rewards pay once, and the quest sheet matches project format.
