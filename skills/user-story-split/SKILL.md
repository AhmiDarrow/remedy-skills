---
name: user-story-split
version: 1.0.1
description: >
  Split an epic or oversized ticket into thin vertical stories that each deliver testable behaviour. Use when work is too big to estimate, finish in one iteration or review safely.
author: Remedy Official
license: Apache-2.0
tags:
  - product
  - planning
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: user-story-split
  official: true
  security_flags: []
---

# User Story Split

## When to use
A backlog item hides several outcomes, or the proposed split is by layer (database, API, UI).

## Steps
1. Read the epic and linked material. Restate who needs what and why in two sentences; list unknowns as questions instead of inventing rules.
2. Walk the user's path end to end and list the steps, variations, roles, data types and error cases.
3. Build the thinnest slice that crosses every needed layer and produces a result a real user or tester can observe.
4. Cut the rest along the seam that fits: workflow step, business rule, happy path before exceptions, one data type or platform before others, manual operation before automation, read before write.
5. Check each story: can ship or be demonstrated alone, fits in an iteration, has value or retires a named risk, and can be reordered without breaking everything.
6. Give each a title, user outcome and a few acceptance criteria with concrete examples, including the relevant failure and permission case.
7. Where the team cannot estimate because something is unknown, add a time-boxed spike with the question it must answer.
8. Order by learning and value: riskiest assumption early, polish and rare variants late. Mark which stories could be dropped while the release stays useful.
9. List non-goals and real dependencies, and check that every part of the epic lands in a story or is explicitly excluded.

## Watch out for
- "Build the backend" and "build the screen" are tasks; neither delivers behaviour alone.
- Deferring authorisation, validation or data safety to a later story leaves the first slice unshippable.
- Splitting until each story needs three others to mean anything.
- Writing the solution into every story, which blocks better implementations.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every part of the epic maps to a story or a non-goal, each story has testable criteria and observable value, and the order and open questions are stated.
