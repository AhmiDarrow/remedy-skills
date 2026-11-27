---
name: stuck-loop-breaker
version: 1.0.0
description: >
  Recognise repeated failing attempts and change approach, gather new information or ask for help. Use when the same error keeps returning after several fixes or edits are going back and forth.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - agent-workflow
  - troubleshooting
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - todo
  - web.search
  - owner.notify
metadata:
  source: library
  library_id: stuck-loop-breaker
  official: true
  domain: tooling
  security_flags: []
---

# Stuck Loop Breaker

## When to use
Three attempts at the same obstacle without new understanding is the signal.
## Steps
1. Stop editing. List each attempt, its exact result and what it was supposed to prove.
2. Compare errors literally. An identical message suggests the change never took effect or targets the wrong cause; a changed one is information.
3. Identify the shared assumption behind all attempts and test it directly: right file, right process, right version, real permission, command actually ran.
4. Return to the last known good state, preserving anything useful. Revert only your own changes, never the user's uncommitted work.
5. Get new information of a different kind: the dependency's source at the installed version, a smaller reproduction, verbose output, the project history, an upstream issue.
6. Choose a materially different route and say what result would make you abandon it. Set an attempt or time limit.
7. If the obstacle is a permission, credential, safety block or ambiguous requirement, do not work around it; ask.
8. When asking, give the goal, evidence, attempts, current theory and the specific decision or input needed, and continue only work that does not depend on it.
## Watch out for
- Retrying an unchanged command hoping for another result.
- Making the symptom vanish by disabling a check, forcing a flag or deleting the failing test.
- Redefining the goal to match what works and not saying so.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Either new evidence has opened a route that makes progress, or the user has a concise account with one answerable question.
