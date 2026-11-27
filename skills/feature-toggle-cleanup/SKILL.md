---
name: feature-toggle-cleanup
version: 1.0.1
description: >
  Remove stale feature flags by confirming each one's live value in every environment, then deleting the losing code path and its config. Use when old flags clutter the code or a rollout has finished.
author: Remedy Official
license: Apache-2.0
tags:
  - product
  - quality
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: feature-toggle-cleanup
  official: true
  security_flags: []
---

# Feature Toggle Cleanup

## When to use
Flags have outlived their rollout and nobody is sure which branches still run.

## Steps
1. List flag keys from both sides: the code (`grep` for the evaluation calls, wrappers and constants) and the flag store or config files. Keys present on only one side are findings too.
2. For each, get the real value and targeting in every environment, tenant and segment. The code default says nothing about production. Ask the user for an export if you cannot read the store.
3. Check evaluation data for recent reads and which value they returned. No access means unknown, not unused.
4. Classify: fully on, fully off, still targeted, permanent operational switch, or unknown. Only the first two are candidates.
5. Look for other consumers: other repositories, infrastructure config, analytics queries, tests, runbooks, and older client versions still installed.
6. Get the user to confirm the winning value per flag.
7. Remove one flag per change: replace the check with the winner, delete the losing branch, then follow what became unused (functions, assets, strings, dependencies, test cases).
8. Search for the key as a string again, including dynamically built names such as a prefix plus a variable, then run tests and build.
9. Deploy the code first. Delete the key from the flag store only after no running version reads it, and only with approval.

## Watch out for
- Deleting the stored key first sends running instances to the code default, which may switch a launched feature off.
- Negated flags such as `disable_x` invite keeping the wrong branch; write out in words what users get before editing.
- A flag that has been off for a year may be an emergency kill switch, so ask its owner.
- Database columns or events used only by the dead path need their own, later removal.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each removed flag has a recorded confirmed value, no code or config references remain, tests pass, and flags left in place are listed with the reason.
