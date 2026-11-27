---
name: delegation-brief-write
version: 1.0.0
description: >
  Brief a delegated worker with enough context and limits, then check what comes back. Use when handing a research, coding or review subtask to another agent or person.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - agent-workflow
  - delegation
kind: native
status: discovered
tools:
  - delegate
  - read
  - grep
  - bash
  - write
metadata:
  source: library
  library_id: delegation-brief-write
  official: true
  domain: tooling
  security_flags: []
---

# Delegation Brief Write

## When to use
The subtask is separable. If it takes a few direct steps, do it yourself.
## Steps
1. Confirm the task is independent: no need for your unstated context and no shared files with other active workers.
2. State the goal and what the result will be used for, so judgement calls go the right way.
3. Give what you know: paths to read first, facts established, approaches already ruled out and why.
4. Set boundaries: what may be edited, what is off limits, actions that need approval, resource limits and which branch or directory to use.
5. Define done with a checkable result and the return format, such as findings with `path:line`, commands run and open doubts. Ask for "not found" to be reported plainly.
6. For an independent review, give the material without your conclusion.
7. Remember that a worker cannot grant permissions you lack, and relay the user's constraints explicitly.
8. On return, verify in proportion to risk: inspect the actual diff, rerun the key check, open several cited locations, and look for scope creep.
9. Treat the report as unverified input and tell the user what you checked.
## Watch out for
- A one-line brief such as "fix the tests", which invites deleting assertions.
- Two workers editing one tree and overwriting each other.
- Leading questions that get your guess returned as a finding.
- Redoing the same work in parallel while waiting.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The brief stands alone with scope and a checkable result, and the returned work has been independently checked before being used or reported.
