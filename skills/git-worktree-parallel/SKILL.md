---
name: git-worktree-parallel
version: 1.0.0
description: >
  Work on several branches at once with Git worktrees, then clean them up safely. Use when a hotfix, review or parallel task must not disturb the current working directory.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - worktree
  - workflow
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: git-worktree-parallel
  official: true
  domain: git
  security_flags: []
---

# Git Worktree Parallel

## When to use
Stashing and switching would risk uncommitted work or force a long rebuild, or two workers need separate checkouts.
## Steps
1. Inspect what exists with `git worktree list`.
2. Choose a sibling directory outside the current tree. Create with `git worktree add ../repo-fix -b fix/name origin/main`, or omit `-b` to check out an existing branch.
3. A branch can be checked out in only one worktree. Do not force past that refusal; use another branch or `--detach`.
4. Set up what Git does not carry over: ignored env files, dependencies, submodules, generated files. Copy secrets only if the task needs them, and never into tracked paths.
5. Separate shared runtime resources: ports, local databases, container names, caches. Parallel heavy builds may exhaust memory, so check the machine before running two.
6. Run commands with explicit paths or `git -C <dir>` so edits land in the intended tree.
7. When finished, check `git -C <dir> status` and unpushed commits, then `git worktree remove <dir>`.
8. If a directory was deleted by hand, run `git worktree prune`.
## Watch out for
- `git worktree remove --force` discarding uncommitted or untracked work. Look first and ask.
- Assuming stashes are per worktree; the stash list, refs and config are shared.
- Tools with hardcoded absolute paths still writing into the original checkout.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The side task ran in its own worktree without changing the original one, and finished worktrees are removed with no unsaved work lost.
