---
name: long-task-context-budget
version: 1.0.0
description: >
  Keep a long multi-step task on track with limited working context by controlling what is read and saving state to disk. Use when a job spans many files, hours or possible interruptions.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - agent-workflow
  - context
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
  - write
  - edit
  - todo
  - delegate
  - memory.save
metadata:
  source: library
  library_id: long-task-context-budget
  official: true
  domain: tooling
  security_flags: []
---

# Long Task Context Budget

## When to use
A migration, audit or large feature where early facts will be forgotten before the end.
## Steps
1. Write a state file at the start in a location the project allows: goal in the user's words, constraints, done criteria and the step list. Do not commit it unless asked.
2. Search before reading. Use `grep` to find the lines, then read the needed ranges, not whole large files.
3. Keep command output small with quiet flags or by writing to a log and reading the relevant part. Preserve the failing section and exit status.
4. Delegate wide, noisy exploration when only the conclusion matters, asking for findings with file locations.
5. After each milestone record decisions with reasons, files changed, commands that verified them, dead ends and the next action.
6. Record exact identifiers (paths, branch, commit, job ids); paraphrases cannot be resumed from.
7. After any interruption or summary, reread the state file and check it against `git status` and the actual files before editing.
8. Process large sets in batches with a checklist of items done and remaining, so none is repeated or silently skipped.
9. Put only durable facts in `memory.save`, never secrets.
## Watch out for
- Trusting a remembered file's contents after others or tools may have changed it.
- A progress log listing intentions as completed work.
- Dropping a constraint given early, such as "do not push".
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh worker could resume from the state file and repository alone, and the final result is checked against the original constraints.
