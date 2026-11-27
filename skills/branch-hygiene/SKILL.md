---
name: branch-hygiene
version: 1.0.1
description: >
  Safely clean up merged and stale local Git branches, including squash-merged ones, and start the next branch from an up-to-date base. Use when branches have piled up.
author: Remedy Official
license: Apache-2.0
tags:
  - git
kind: native
status: discovered
tools:
  - bash
metadata:
  source: library
  library_id: branch-hygiene
  official: true
  security_flags: []
---

# Branch Hygiene

## When to use
The local branch list is cluttered or the user is about to start new work.

## Steps
1. Run `git status` and `git worktree list`. Note the current branch, a detached HEAD and branches held by worktrees.
2. Run `git fetch --prune`, then find the default branch with `git symbolic-ref refs/remotes/origin/HEAD`. If unset, check the remote with `git remote show origin`.
3. List everything: `git for-each-ref --format="%(refname:short) %(upstream:short) %(upstream:track) %(committerdate:short)" refs/heads`.
4. Group branches. Merged by ancestry: `git branch --merged origin/<default>`. Upstream shown as `[gone]`: the remote branch was deleted, which does not prove the work landed. No upstream: may be the only copy.
5. For squash or rebase merges, which ancestry misses, check the pull request state on the host (for example `gh pr list --state merged --head <branch>`), and confirm the local tip equals the merged head so later commits are not lost. `git cherry origin/<default> <branch>` helps but cannot match several commits squashed into one.
6. Show a table with branch, tip hash, last commit date and evidence. Get approval for the deletion list.
7. Delete with `git branch -d`. Use `-D` only for branches whose merge was proven another way or that the user chose to discard, and keep the printed hashes for recovery.
8. For the next task, follow the repository's naming pattern and run `git switch --no-track -c <name> origin/<default>`.

## Watch out for
- Protected, release and long-lived branches also appearing in the merged list; exclude them.
- `git branch -d` judging against the upstream or current HEAD, not necessarily the default branch.
- Deleting remote branches: a separate action affecting others that needs its own approval.
- Removing a worktree that contains uncommitted files.
- Force-pushing the default branch or hard-resetting shared branches; cleanup never needs either.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Only approved branches are gone, each deleted tip hash is reported, unproven branches remain, and any new branch starts at the fetched base.
