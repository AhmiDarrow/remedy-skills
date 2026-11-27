---
name: implementation-plan-write
version: 1.0.0
description: >
  Write a step-by-step implementation plan grounded in the actual files, with a check after each step. Use when a multi-file change needs a plan before editing or will be executed by someone else.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - planning
  - documentation
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
  - todo
metadata:
  source: library
  library_id: implementation-plan-write
  official: true
  domain: tooling
  security_flags: []
---

# Implementation Plan Write

## When to use
The change spans several files or sessions, or a different worker will carry it out without your context.
## Steps
1. Trace the current behaviour from entry point to side effect and note the files and functions involved. A plan written without opening them is a wish.
2. State the goal as observable behaviour and list what must not change.
3. Search for every caller, implementation, config key, fixture and doc that mentions what you will change; put them in the plan.
4. Order steps so the build and tests pass after each one. Additive changes come first (new field, new path), switching callers second, deleting the old path last.
5. For each step write the files, the change in a sentence or two, and the exact command or manual check that shows it worked.
6. Flag steps that are irreversible or touch stored data, and give each a backup or rollback line.
7. List open questions separately; never bury a guess inside a step.
8. Reread as a stranger. Any step containing "update as needed" or "handle edge cases" is not yet planned; name the files and cases.
## Watch out for
- A final step called "add tests" and another called "fix remaining issues". Checks belong to the step that creates the risk.
- Pasting large code blocks that will be wrong once the file is edited. Give signatures and decisions, not full implementations.
- Continuing to follow the plan after the code proves it wrong; amend it and note why.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each step names real paths, leaves the project in a working state and has its own verification, and all known call sites appear somewhere in the plan.
