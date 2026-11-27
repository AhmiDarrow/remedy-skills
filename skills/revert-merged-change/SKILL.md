---
name: revert-merged-change
version: 1.0.0
description: >
  Safely undo a change already merged into a shared branch, including merge commits and later re-landing. Use when a merged change broke something and must come out without rewriting history.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - revert
  - release
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: revert-merged-change
  official: true
  domain: git
  security_flags: []
---

# Revert Merged Change

## When to use
The branch is shared, so the fix is a new commit, not a reset.
## Steps
1. Identify exactly what landed: merge commit, squash commit or a series (`git log --first-parent`).
2. Check what came after and depends on it, by searching later commits that use its symbols or files.
3. Check one-way effects first: applied database migrations, new data formats, published packages, sent messages. Reverting code does not undo them and old code may fail on new data. Plan a forward fix or compensating step instead where needed.
4. On an up-to-date branch use `git revert <sha>`. For a merge commit use `git revert -m 1 <merge>`, after confirming with `git show` that parent 1 is the mainline. For a series, revert newest first.
5. Resolve conflicts by removing the bad behaviour while keeping later unrelated work.
6. Build, test and reproduce the original breakage to show it is gone.
7. Write the reason and the broken symptom in the commit message, and open it for review per project rules; push only with approval.
8. To re-land after a reverted merge, first revert the revert (or rebuild the commits afresh), then add the fix. Merging the old branch again will not bring back the reverted changes, because Git considers them merged.
## Watch out for
- Removing a database column or file format support that existing data now needs.
- Force-pushing the shared branch to make the commit vanish.
- A leaked secret: reverting leaves it in history, so it must be rotated.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The shared branch no longer shows the breakage, checks pass, irreversible effects are handled, and the re-land route is noted.
