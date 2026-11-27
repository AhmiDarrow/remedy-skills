---
name: critical-path-schedule
version: 1.0.0
description: >
  Build a dependency-based project schedule, find the critical path and show real slack and date risk. Use when a delivery date must be checked against tasks, dependencies and people.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - project
  - scheduling
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: critical-path-schedule
  official: true
  domain: data
  security_flags: []
---

# Critical Path Schedule

## When to use
A project has linked tasks and someone needs to know whether the date holds.

## Steps
1. List tasks that each produce a checkable result, with duration in working days from those doing the work. Include reviews, approvals, procurement and waiting time.
2. For each, record real predecessors. Separate technical necessity from habit.
3. Check for cycles, missing links and tasks that connect to nothing.
4. Forward pass: earliest start is the latest earliest finish of predecessors. Backward pass from the end gives latest times. Slack is the difference; the zero-slack chain, when the end is the computed finish, is critical.
5. Compute with a short script or sheet, using a working calendar with holidays and leave.
6. Check resources: two parallel tasks for one person are not parallel. Re-sequence and recompute.
7. Report near-critical paths and the least certain durations, with optimistic and pessimistic dates.
8. If the date fails, show options: cut scope, move a dependency, overlap with stated rework risk, or move the date.

## Watch out for
- Starting from the deadline and shrinking durations to fit.
- Confusing effort with elapsed duration for part-time people.
- Assuming new people shorten critical work immediately.
- A schedule never updated with actuals, so the critical path shown is stale.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every task is linked, the critical path and slack are computed on a real calendar with resource conflicts resolved, and the date risk is stated.
