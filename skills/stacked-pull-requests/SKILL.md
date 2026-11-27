---
name: stacked-pull-requests
version: 1.0.0
description: >
  Manage a chain of dependent pull requests, restacking after review changes and merges. Use when later work builds on a branch that is still in review.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - pull-requests
  - workflow
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: stacked-pull-requests
  official: true
  domain: git
  security_flags: []
---

# Stacked Pull Requests

## When to use
One large change is delivered as steps, each branch based on the previous one.
## Steps
1. Record the order: base, part 1, part 2, and so on. Each part must build and make sense alone.
2. Set each pull request's base to the branch below it, so its diff shows only its own commits. State the position in the stack in each description.
3. To change a lower part, commit there, then rebase upward. With Git 2.38 or later, `git rebase --update-refs` from the top branch moves the intermediate branch pointers along.
4. Before any rebase, note each branch tip so you can recover, and verify with `git range-diff` that only intended commits changed.
5. Merge from the bottom up.
6. After a squash or rebase merge of the bottom part, its original commits are no longer in the base's history. Replay only the next part's own commits: `git rebase --onto origin/main <old-part1-tip> part2`.
7. Retarget the next pull request's base to the main branch, and do so before deleting the merged branch.
8. Push each rewritten branch with `--force-with-lease`, after approval, and rerun checks.
## Watch out for
- A plain rebase after a squash merge, which replays already merged commits and produces conflicts against yourself.
- Stacks so deep that one early review comment costs hours; merge lower parts promptly.
- Someone else's commits on a middle branch being overwritten.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every open pull request shows only its own changes against the right base, and merged parts leave no duplicated commits above.
