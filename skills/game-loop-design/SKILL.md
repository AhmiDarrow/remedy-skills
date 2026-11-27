---
name: game-loop-design
version: 1.0.1
description: >
  Design or diagnose a core gameplay loop by mapping verbs, decisions, feedback, rewards and failure, then testing it in a prototype. Use when a game feels repetitive, aimless or not yet fun.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - design
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: game-loop-design
  official: true
  domain: gaming
  security_flags: []
---

# Game Loop Design

## When to use
The moment-to-moment cycle is undefined or fails to keep players interested.

## Steps
1. State in one line what the player is trying to do and the intended feeling.
2. Write the short loop as a table: situation, available verbs, decision, result, feedback, reward and what changes the next situation. Add its duration.
3. Test each decision: are there at least two options that are right under different conditions? If one always wins, name it.
4. Connect the short loop to a session goal and a long-term goal. Each outer loop should feed new situations or choices back inward, not only bigger numbers.
5. Define failure: causes, what is lost, how the player learns why, time to retry and how to avoid a death spiral where losing makes losing likelier.
6. Check runaway success too, where winning removes all challenge.
7. Walk through 5, 20 and 60 minute sessions plus first-time, returning, expert and interrupted players.
8. Specify the smallest prototype of the short loop without progression rewards or final art. Say what observation counts as success, for example testers choosing to replay unprompted.
9. After tests, change the weakest link and record what was tried.

## Watch out for
- Using unlocks or daily rewards to cover a core action that is dull by itself.
- A feature list presented as a loop, with no verbs or decisions.
- Compulsion tricks such as punishing absence offered as engagement.
- Declaring the loop fun from a document; only play shows it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The loop table, outer-loop links, failure and runaway rules and a prototype test with pass criteria are written.
