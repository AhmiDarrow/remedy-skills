---
name: state-machine-spec
version: 1.0.0
description: >
  Model a lifecycle as explicit states and transitions so illegal and forgotten cases become visible. Use when an order, job, connection or document has status flags that drift into impossible combinations.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - state-machine
  - architecture
kind: native
status: discovered
tools:
  - read
  - grep
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: state-machine-spec
  official: true
  domain: backend
  security_flags: []
---

# State Machine Spec

## When to use
Booleans like `isPaid`, `isCancelled` and `isShipped` can contradict each other, or bugs appear when events arrive late or twice.
## Steps
1. Search for every write to the status fields and list who writes, on what trigger.
2. Name the states as mutually exclusive conditions of one entity. Query existing data for flag combinations in use and map each to a state or flag it as corrupt.
3. List events, including the boring ones: timeout, retry, user cancel, process restart, duplicate delivery.
4. Build a state-by-event grid. Every cell gets a target state plus side effect, "ignore", or "error". Empty cells are the bugs.
5. For in-between states (sending, processing) define what recovers an entity stranded there after a crash.
6. Put transitions in one function that takes current state and event and returns the new state; make other code call it.
7. Persist transitions conditionally, for example an update that matches both id and expected old state, and treat zero affected rows as a lost race.
8. Test the grid exhaustively, including that illegal transitions are refused.
## Watch out for
- A state called "error" with no way out and no record of where it came from.
- Performing the side effect before the transition is durably recorded, so a retry repeats it.
- Mapping old data to new states without a rule for the contradictory rows.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every state-event pair has a defined result, all status writes go through the transition function, and tests cover both allowed and refused transitions.
