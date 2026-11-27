---
name: spike-timebox-experiment
version: 1.0.0
description: >
  Run a time-boxed throwaway experiment that answers one technical question with evidence. Use when a design choice depends on whether something works, performs or integrates as hoped.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - planning
  - prototyping
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - web.fetch
  - todo
metadata:
  source: library
  library_id: spike-timebox-experiment
  official: true
  domain: tooling
  security_flags: []
---

# Spike Timebox Experiment

## When to use
"Can this library stream 2 GB files?" or "Will this parser handle our oldest documents?" Reading more will not settle it.
## Steps
1. Write the question so it has a yes, no or number as its answer, plus the threshold that counts as yes (for example "under 200 ms for the largest real file").
2. Set a time box up front, typically half a day or less, and say what happens if it expires unanswered.
3. Work in a scratch directory or a branch that will not be merged. Keep production code untouched.
4. Attack the hardest part first. Skip error handling, structure and tests that do not help answer the question.
5. Feed it realistic worst-case input, not a toy. Note the machine, versions and data size used.
6. Measure with a repeatable command and run it more than once; report the spread.
7. At the time box, stop. Report the answer, the evidence, what was not covered, and the recommended decision.
8. Keep the command and the findings; discard the code. If the approach is adopted, rebuild it properly.
## Watch out for
- A spike quietly becoming the implementation, carrying its missing error paths with it.
- Moving the success threshold after seeing the result.
- Proving the happy path while the real doubt (concurrency, large input, offline, permissions) stays untested.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The original question has an answer with a reproducible measurement behind it, or a clear statement that the time box ran out and what remains unknown.
