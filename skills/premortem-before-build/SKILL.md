---
name: premortem-before-build
version: 1.0.0
description: >
  Imagine a plan has already failed, work out why, and turn the likely causes into changes or tripwires. Use before committing to a risky migration, rewrite, launch or architecture change.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - planning
  - risk
kind: native
status: discovered
tools:
  - read
  - grep
  - write
  - todo
metadata:
  source: library
  library_id: premortem-before-build
  official: true
  domain: tooling
  security_flags: []
---

# Premortem Before Build

## When to use
The plan looks reasonable and everyone is optimistic, but reversing course later would be expensive.
## Steps
1. Write the failure as fact with a date: "Six weeks from now we abandoned this migration." Vague futures produce vague causes.
2. Generate causes independently across lenses: data (old, dirty, huge), compatibility (old clients, saved files), operations (deploy order, rollback), performance, dependencies, people (single owner, review bottleneck), and scope growth.
3. Rewrite each cause as a mechanism. "Performance problems" becomes "the backfill locks the orders table longer than the request timeout".
4. Check the plausible ones against the repo and plan now; some can be proven or ruled out in minutes.
5. Rank by likelihood and damage, and keep the top five or so.
6. For each choose one action: change the plan, add an early test, set a tripwire (a measurable signal with a threshold and the response), or accept it explicitly.
7. Decide the abort condition: what observation would make you stop and roll back, and confirm rollback is possible at that point.
8. Add the actions to the task list with owners.
## Watch out for
- Stopping at a list of fears with no change to the plan.
- Only technical causes; "reviewer unavailable for two weeks" sinks plans too.
- A rollback that exists only on paper, for example after new writes already use a format the old code cannot read.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each top-ranked failure has a plan change, test, tripwire or recorded acceptance, and an abort condition with a feasible rollback is written down.
