---
name: rice-priority-scoring
version: 1.0.0
description: >
  Score candidate features with reach, impact, confidence and effort, then stress-test the ranking. Use when a backlog needs a transparent, comparable priority order.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - product
  - prioritization
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: rice-priority-scoring
  official: true
  domain: data
  security_flags: []
---

# Rice Priority Scoring

## When to use
Several candidates compete and the team wants its assumptions visible.

## Steps
1. Confirm the outcome being optimised; scores for different goals cannot be compared.
2. Rewrite candidates at similar size and as problems solved.
3. Reach: affected users or events in one fixed period, with the data source.
4. Impact: a small fixed scale, with a written example of what each level means, applied per reached user.
5. Confidence: tie levels to evidence, such as usage data, interviews or opinion only.
6. Effort: total person-time across all roles, estimated by those who would do it.
7. Compute reach * impact * confidence / effort in a sheet that keeps the inputs.
8. Vary the shakiest inputs. Where rank flips easily, call it a tie and name what to learn.
9. Pull out mandatory work (legal, security, contractual) and dependencies; show them separately.

## Watch out for
- Tuning inputs until a favourite wins.
- Mixing monthly reach for one item with yearly for another.
- Presenting 41.7 versus 40.2 as a real difference.
- Ranking without capacity; the score does not say what fits.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every score has sourced or explicitly guessed inputs, sensitive ties are marked, and mandatory items are separate.
