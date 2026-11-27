---
name: batch-pr-integration
version: 1.0.0
description: >
  Combine several waiting pull requests on one integration branch, test them together and land them safely. Use when multiple approved changes overlap or testing each one separately is too slow.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - pull-requests
  - integration
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
  - todo
metadata:
  source: library
  library_id: batch-pr-integration
  official: true
  domain: git
  security_flags: []
---

# Batch Pr Integration

## When to use
Each change passes alone; nobody has seen them together.
## Steps
1. List candidates with head commit, base age, check status and touched files. Exclude drafts and ones with unresolved review concerns.
2. Find overlaps by file and by shared symbols, schema versions or numbered migrations, which often collide without a textual conflict.
3. Order them: foundations and fixes first, wide mechanical changes last or first deliberately.
4. Create an integration branch from the freshly fetched target.
5. Merge one at a time, keeping a separate merge commit per change so any one can be removed. After each, run the fast build to pin breakage to its cause. `git merge-tree --write-tree A B` (Git 2.38 or later) can preview conflicts.
6. When two changes add the same id, version number or registry entry, renumber one and check references.
7. Run the full gate once on the final tree.
8. On failure, find the culprit using the merge sequence; fix it, or rebuild the branch without that change.
9. Report what is included and excluded. Merge only with approval, and confirm the target has not moved since testing.
## Watch out for
- Fixes made only on the integration branch for a problem the source change still carries.
- Squashing the batch into one commit, losing attribution and revertability.
- Landing a tree different from the tested one.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The exact final tree passed the full gate, each included change is identifiable, and exclusions have stated reasons.
