---
name: split-commits-before-review
version: 1.0.0
description: >
  Reorganise a messy branch into small logical commits without losing or changing any work. Use when one branch or commit mixes unrelated changes that reviewers or future bisects need separated.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - history
  - review
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: split-commits-before-review
  official: true
  domain: git
  security_flags: []
---

# Split Commits Before Review

## When to use
"WIP" and "fix" commits, or a refactor tangled with a behaviour change.
## Steps
1. Confirm nobody else builds on the branch. Rewriting shared history needs their agreement.
2. Commit or stash everything, then create a safety ref: `git branch backup/topic`.
3. List the target commits in order: mechanical moves and renames first, preparatory refactors, then behaviour with its tests.
4. Reset to the merge base in the default mixed mode: `git reset $(git merge-base HEAD origin/main)`. Changes stay in the working tree, unstaged; substitute the real base.
5. Stage per group by path. Within a file use `git add -p`, which is interactive; without an interactive terminal, write the wanted hunks to a patch and apply it with `git apply --cached`.
6. Before each commit review `git diff --cached`. Remember new files are untracked after the reset and need adding.
7. Verify each commit builds on its own, for example by checking it out in a separate worktree, or with `git rebase --exec "<test command>" <base>`.
8. Compare the end state: `git diff backup/topic HEAD` must be empty.
9. Push rewritten history only after approval, using `git push --force-with-lease`.
## Watch out for
- Testing the staged commit while unstaged later changes are still in the tree and propping it up.
- Silently losing a new or deleted file during regrouping.
- Hooks that reformat files and make the final diff differ; inspect it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each commit has one purpose and passes the build, the final tree equals the backup, and nothing was force-pushed without approval.
