---
name: adr-write
version: 1.0.1
description: >
  Write an architecture decision record with context, forces, real options, the decision, consequences and a revisit trigger, in the repository's own convention. Use when a significant technical choice is made or proposed.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - architecture
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: adr-write
  official: true
  security_flags: []
---

# Adr Write

## When to use
A choice is costly to reverse, affects several parts or teams, or keeps being re-argued.

## Steps
1. `glob` for existing records (such as `docs/adr/` or `docs/decisions/`) and follow their template, numbering and status words. If none exist, propose a location before creating it.
2. Search existing records and code for earlier decisions on this topic. Use `git log` to find when the current approach arrived and why.
3. Establish who decides and whether this is still proposed or already accepted. Never mark accepted on your own.
4. Write a title naming the choice, with date and status.
5. Context: the problem, forces and constraints as true at that time (load, team, deadlines, compliance, existing systems), with evidence and unknowns.
6. List the decision criteria, then the genuine options, including keeping things as they are. Compare each against the same criteria, giving the rejected ones a fair case.
7. State the decision in a direct sentence with its scope and what it does not cover.
8. Record consequences both ways: gains, costs, new risks, follow-up work, migration and how to back out.
9. Say how compliance will be checked and what observation would reopen the decision.
10. Keep it to a page or two, one decision per record, linked from the index and related docs. To change an accepted decision, add a new record that supersedes it and update only the old one's status and link.

## Watch out for
- Reconstructing reasons for a past decision and presenting them as recorded fact; mark it retrospective.
- Strawman alternatives and consequence lists with no downsides.
- A design document disguised as a record; link long detail.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A record in the project's convention states context, compared options, decision, trade-offs, status, decider and revisit trigger, with links updated and unverified claims marked.
