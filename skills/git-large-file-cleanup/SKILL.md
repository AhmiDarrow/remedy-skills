---
name: git-large-file-cleanup
version: 1.0.0
description: >
  Find what bloats a Git repository and fix it, including the careful path for rewriting history. Use when clones are slow, the repo is huge or a large binary was committed.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - repo-hygiene
  - storage
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: git-large-file-cleanup
  official: true
  domain: git
  security_flags: []
---

# Git Large File Cleanup

## When to use
Deleting the file in a new commit does not shrink history.
## Steps
1. Measure: `git count-objects -vH`.
2. List the largest blobs with paths: `git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectsize) %(objectname) %(rest)'`, keep blob lines and sort numerically by size (Git Bash or a Unix shell).
3. For each, decide: still needed, build output, dependency, test asset or accident. Check whether it was ever pushed.
4. If it exists only in unpushed commits, amend or rebase those commits; no shared rewrite is needed.
5. Stop future growth with ignore rules, a size check in hooks or CI, and external storage or Git LFS for needed binaries (note that hosts may limit LFS storage).
6. Before any shared history rewrite, tell the user the cost: new hashes, broken open pull requests and clones, invalid signatures and tag moves. Get explicit approval.
7. Rewrite on a fresh mirror clone with `git filter-repo` (installed separately) or `git lfs migrate`, keeping an untouched backup.
8. Verify the current tree is as expected, builds work and size dropped. Coordinate the force push, and have collaborators re-clone so old objects do not return.
9. Ask the host whether cached objects or forks still hold the data.
## Watch out for
- One stale clone merging the old history back in.
- Removing a path that old release tags need in order to build.
- Treating a rewrite as enough for a leaked credential; rotate it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cause is prevented, and either the bloat is knowingly left or the approved rewrite is verified on a fresh clone with a retained backup.
