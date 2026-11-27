---
name: fork-upstream-sync
version: 1.0.0
description: >
  Bring a long-lived fork or patched vendored copy up to date with upstream while keeping local changes. Use when a fork has fallen behind or local patches must be carried to a new upstream release.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - fork
  - maintenance
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
  - write
metadata:
  source: library
  library_id: fork-upstream-sync
  official: true
  domain: git
  security_flags: []
---

# Fork Upstream Sync

## When to use
Local patches matter, and a careless sync would drop or duplicate them.
## Steps
1. Check remotes with `git remote -v`; add `upstream` if missing, then `git fetch upstream --tags`.
2. Pick a target: a release tag is usually easier to reason about than the moving default branch.
3. Inventory local changes: `git log --oneline --no-merges <target>..HEAD` and `git cherry -v <target>`, which marks patches already present upstream. Squashed or edited upstream versions may not be detected, so check those by content.
4. Record for each patch its purpose and verdict: drop (upstream has it), keep, or rework.
5. Choose the method by who consumes the fork: merge if others pull it, rebase the patch series if it is kept as a clean stack and rewriting is acceptable.
6. Work on a new branch. Resolve conflicts with upstream's new structure as the base, reapplying your intent.
7. Compare old and new patch series with `git range-diff`.
8. Read upstream release notes for breaking changes, then run both upstream tests and tests covering your patches.
9. Update the patch inventory file and note patches worth sending upstream.
## Watch out for
- A web "sync" or discard button that deletes local commits.
- A patch that still applies but now does nothing because upstream moved the code path.
- Pushing to the upstream remote by mistake; check push targets.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The new branch contains the chosen upstream version, every local patch has a recorded verdict and the kept ones are shown working.
