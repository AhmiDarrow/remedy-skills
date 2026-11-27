---
name: rebase-onto-main
version: 1.0.1
description: >
  Bring a feature branch up to date with the main branch by rebase or merge, safely handling conflicts and rewritten history. Use when a branch is behind or its base was squash-merged.
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
  library_id: rebase-onto-main
  official: true
  security_flags: []
---

# Rebase Onto Main

## When to use
A branch needs the latest base changes before review or merge.

## Steps
1. Check `git status` and for an operation already in progress. Commit work or, with consent, stash it, including untracked files with `-u` if needed.
2. Detect the default branch from `refs/remotes/origin/HEAD`, confirm it is the intended base, and run `git fetch origin`.
3. Decide rebase or merge. Rebase suits a branch only this user builds on. If others have commits or work based on it, merge or agree first. Compare the local branch with its remote so their commits are not dropped.
4. Record the starting point with a local tag, `git tag backup/<name>`, and note its hash. Use a tag because `--update-refs` (or the `rebase.updateRefs` setting) can move a backup branch. Inspect `git log --graph --oneline origin/<base> HEAD` and note any merge commits; a plain rebase flattens them, while `--rebase-merges` keeps the structure.
5. Run `git rebase origin/<base>`. If the branch was stacked on another that has been squash-merged, replay only your commits: `git rebase --onto origin/<base> <old-parent-tip> <branch>`.
6. At each conflict remember "ours" is the new base side and "theirs" is the commit being replayed. Resolve by intent, stage only resolved files and `git rebase --continue`. Use `--abort` if the direction is wrong.
7. Compare before and after with `git range-diff origin/<base> backup/<name> HEAD`. Explain unexpected changes or missing commits. For the stacked case, give explicit old and new ranges.
8. Regenerate derived files, then build and test the result.
9. If already pushed, ask before `git push --force-with-lease --force-if-includes` (needs a recent Git), naming the remote branch. Never force-push the default branch.

## Watch out for
- A background fetch weakening a bare `--force-with-lease`: the remote-tracking ref moves even though you never integrated those commits.
- Two migrations or version entries merging without a textual conflict but in the wrong order.
- Running `git pull` after a rebase and merging the old commits back in.
- With stacked branches, forgetting the others; recent Git offers `--update-refs`.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The branch sits on the fetched base or has it merged, the range comparison is explained, tests pass, and any force push was approved or left pending.
