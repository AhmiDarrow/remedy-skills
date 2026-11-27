---
name: merge-conflict-resolve
version: 1.0.0
description: >
  Resolve Git merge or rebase conflicts by reconstructing what both sides intended, including lock files. Use when a merge, rebase, cherry-pick or stash pop stops with conflicts.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - merge-conflicts
  - workflow
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: merge-conflict-resolve
  official: true
  domain: git
  security_flags: []
---

# Merge Conflict Resolve

## When to use
Picking "ours" or "theirs" by reflex silently throws away someone's work.
## Steps
1. Run `git status` to learn which operation is in progress and list unmerged paths. Note the abort command (`git merge --abort`, `git rebase --abort`, `git cherry-pick --abort`) before editing. A conflicted stash pop has no abort (the stash entry is kept), and a merge started with uncommitted changes may not abort cleanly, so ask before discarding anything.
2. Get the base in the markers: `git checkout --conflict=diff3 -- path` rewrites the file with all three versions. It discards edits already made to that file's conflict.
3. For each side read why it changed: `git log --merge -p -- path` during a merge.
4. During a rebase the labels feel reversed: "ours" is the branch you are rebasing onto, "theirs" is your commit being replayed.
5. Write a result that keeps both intents. If they truly contradict, ask the user.
6. Handle non-text cases deliberately: delete against modify (was the file moved? apply the edit at its new home), binaries (choose one side and say which).
7. For lock files do not hand-merge. Resolve the manifest first, take one side's lock file, then let the package manager update it (for example `npm install --package-lock-only`, a plain `pnpm install` or `yarn install`, `go mod tidy` for go.sum, a normal build for Cargo.lock). Check no unrelated versions jumped.
8. Search for leftover markers (`git diff --check`), keep each file's line endings, then build and test before staging the final continue.
## Watch out for
- Text merging cleanly but meaning breaking: one side renames a function, the other adds a call to the old name. Grep for it and compile.
- `git add -A` sweeping in stray files during the resolution.
- The same conflict repeating through a long rebase; `git config rerere.enabled true` records resolutions, but review what it replays.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No unmerged paths or markers remain, both sides' intended behaviour is present, and the build and tests pass on the resolved tree.
