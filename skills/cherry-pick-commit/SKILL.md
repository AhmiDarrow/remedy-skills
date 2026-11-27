---
name: cherry-pick-commit
version: 1.0.1
description: >
  Copy specific commits onto another branch, checking hidden dependencies, merge commits and duplicates. Use when backporting a fix or moving selected work without merging the whole branch.
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
  library_id: cherry-pick-commit
  official: true
  security_flags: []
---

# Cherry Pick Commit

## When to use
Only some commits from one branch belong on another.

## Steps
1. Confirm source commits and target branch. Require a clean tree and update the target from its remote.
2. Check what is already there: `git cherry -v <target> <source>` marks patch-equivalent commits with `-`. Also search for earlier backport notes with `git log <target> --grep=<sha>`.
3. Read each commit with `git show --stat <sha>`. Look for dependencies in earlier unpicked commits: `git log <target>..<sha> -- <paths>`.
4. Apply oldest first. For a range, `A..B` excludes A, while `A^..B` includes it. Preview with `git log --reverse --oneline` using the same range.
5. Use `git cherry-pick -x <sha>` when the source commit is public, so the new message records where it came from.
6. For a merge commit, inspect its parents and use `-m <parent-number>`, usually 1 for the mainline side, only after confirming that the resulting diff is what is wanted. Picking the individual commits is often clearer.
7. On conflict, port the intent to the target's code. Do not pull in unrelated source changes to make the patch fit; if a prerequisite is needed, say so and abort with `git cherry-pick --abort`. Continue with `--continue`.
8. If a pick is empty, verify the change is already present before `git cherry-pick --skip`.
9. Build and run tests on the target, then compare with `git range-diff <sha>^! HEAD^!`. Push only when asked.

## Watch out for
- A clean apply that calls a function or relies on a schema the target lacks.
- Leaving out follow-up fixes to the picked commit; search later history for its hash and files.
- Picking a revert or a merge without understanding which change it carries.
- Editing the resolution so heavily that the message no longer describes it; note the adaptation.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The target contains exactly the intended changes, required follow-ups are included, tests pass on that branch, and adaptations or skips are reported.
