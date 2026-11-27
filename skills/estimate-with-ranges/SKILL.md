---
name: estimate-with-ranges
version: 1.0.0
description: >
  Estimate engineering work as a range with stated unknowns instead of a single hopeful number. Use when someone asks how long a change will take or whether a date is realistic.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - planning
  - estimation
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: estimate-with-ranges
  official: true
  domain: tooling
  security_flags: []
---

# Estimate With Ranges

## When to use
A date or effort figure will be used to promise something to someone.
## Steps
1. Restate what "finished" includes: tests, review, docs, migration, release, and any waiting on other people.
2. Break the work into pieces small enough that you have done something like each one. A piece you cannot picture is an unknown, not a number.
3. Inspect the affected code before estimating: count call sites, check for tests, look for generated or vendored files.
4. Find a comparison in history with `git log --stat` for a similar past change: how many files, how many follow-up fixes, how many days between first and last commit.
5. Give each piece a likely case and a bad case. Sum likely cases for the optimistic end; add the bad-case gap for the two or three riskiest pieces for the upper end.
6. Separate effort (hours of work) from elapsed time (review queues, test runs, approvals, other duties).
7. State what would narrow the range and how long that investigation takes. Offer it when the upper end is more than about twice the lower.
8. Say which scope could be dropped to hit a fixed date.
## Watch out for
- Letting the requester's wished-for date anchor the number.
- Quoting only the low end; it is the one that will be remembered.
- Padding silently. Name the risk that justifies the width so it can be removed.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The answer gives a range, separates effort from calendar time, lists what is included, and names the unknowns driving the upper end.
