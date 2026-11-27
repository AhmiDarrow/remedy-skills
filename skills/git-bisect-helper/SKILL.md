---
name: git-bisect-helper
version: 1.0.1
description: >
  Find the commit that introduced a regression with git bisect and a trustworthy test script. Use when something worked in an older version and the cause is not obvious from recent changes.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - debug
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: git-bisect-helper
  official: true
  security_flags: []
---

# Git Bisect Helper

## When to use
There is a known good point, a known bad point and a way to tell them apart.

## Steps
1. Require a clean tree, or use a separate worktree. Record the current branch.
2. Verify both ends by running the check on them, not from memory.
3. Write the check as a script outside the repository, so checkouts do not change it. Exit 0 means good; 125 means this commit cannot be tested and should be skipped; other codes from 1 to 127 mean bad; higher codes abort the run.
4. Make setup failures return 125 only when they are unrelated to the bug. Build from a state that does not reuse stale artifacts, and reinstall dependencies when lock files change.
5. Check for the specific symptom, such as the error text or wrong value, so a different failure is not counted as bad.
6. Start with `git bisect start <bad> <good>`, then `git bisect run <script>`. For manual testing, mark each step `git bisect good`, `bad` or `skip`. Add `--first-parent` to start, if supported, to identify the merge that introduced it.
7. For a flaky symptom, repeat the check enough times that a lucky pass is unlikely, and count any reproduction as bad.
8. Save `git bisect log`. A wrong mark can be fixed by editing the log, resetting and using `git bisect replay`.
9. Inspect the culprit with `git show`. Confirm it by testing its parent and the commit itself, and where practical by reverting it on the bad tip.
10. Run `git bisect reset` and remove only temporary files you created.

## Watch out for
- Exit 127 from a missing command counting as bad and steering the search to the wrong commit.
- Untracked build output carrying results from one commit to the next.
- Databases or caches migrated forward by a newer commit.
- Blaming the found commit when the real change was an unpinned dependency or the environment; the "good" end then fails today too.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The first bad commit, or the smallest range left by skips, is confirmed by rerunning the check, and the repository is back on its starting branch.
