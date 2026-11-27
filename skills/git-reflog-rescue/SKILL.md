---
name: git-reflog-rescue
version: 1.0.0
description: >
  Recover lost commits, deleted branches, dropped stashes or work after a bad reset or rebase. Use when someone thinks Git work has disappeared.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - recovery
  - troubleshooting
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: git-reflog-rescue
  official: true
  domain: git
  security_flags: []
---

# Git Reflog Rescue

## When to use
After `reset --hard`, a botched rebase, a deleted branch or a dropped stash.
## Steps
1. Stop modifying the repository. Do not run `git gc`, `git prune` or reflog expiry. If the stakes are high, copy the whole directory first, including `.git`.
2. Establish what was lost and its last known state: committed, stashed, only staged, or never added.
3. Commits: read `git reflog --date=iso` and the branch's own `git reflog show name`. Entries describe the operation that moved the ref.
4. Inspect candidates with `git log --oneline -5 <sha>` and `git show --stat <sha>` before restoring.
5. Restore onto a new name, `git branch rescue <sha>`, so nothing current is overwritten. Move the original branch only after the user confirms the content.
6. Deleted branches or dropped stashes missing from the reflog: `git fsck --no-reflogs --unreachable`, then inspect the commit objects. Stash entries appear as merge commits. Apply one on a clean new branch with `git stash apply <sha>`.
7. Staged but never committed files may survive as dangling blobs: `git fsck --lost-found`, then search the written files for distinctive text. Names are lost.
8. For never-added changes Git has nothing; check editor local history, backups and file system snapshots, and say plainly if there is no source.
## Watch out for
- Trying `reset --hard` or `git clean` as part of the rescue, which destroys more.
- Expecting a fresh clone to have the old reflog; reflogs are local.
- Delay: unreachable objects are eventually collected.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The recovered content is on a new branch or in a separate directory, verified by the user, or the unrecoverable parts are stated clearly.
