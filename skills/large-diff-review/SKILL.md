---
name: large-diff-review
version: 1.0.0
description: >
  Review a very large pull request systematically without skimming it into approval. Use when a change spans many files and cannot be read carefully top to bottom.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - review
  - risk
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - write
metadata:
  source: library
  library_id: large-diff-review
  official: true
  domain: git
  security_flags: []
---

# Large Diff Review

## When to use
Hundreds or thousands of changed lines, and the honest alternative would be "looks good".
## Steps
1. Get the shape with `git diff --stat` and `--dirstat`, with `-M` so moves appear as renames.
2. Sort files into buckets: generated or vendored, mechanical (renames, formatting), tests, and hand-written logic. Verify the bucket instead of trusting the name.
3. For mechanical parts, reproduce them: run the same formatter or codemod on the base and diff against the branch. Any leftover difference is a hand edit to read closely.
4. For moved code, use `git diff --color-moved=dimmed-zebra` to expose edits hidden inside moves.
5. Read the contracts first: schemas, public types, interfaces, config, migrations. Then the callers.
6. Spend most time on risk: auth, money, deletion, concurrency, persistence formats, error paths.
7. Search the repository for call sites the diff did not touch but should have.
8. If the change mixes unrelated work, ask for a split and say along which lines.
9. State your coverage: files read closely, sampled and not reviewed.
## Watch out for
- Fatigue approving the last third unread; that is where the odd file hides.
- Assuming a lock file or snapshot update is harmless without checking what moved.
- Judging only the added lines; removed validation matters as much.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The review lists findings with locations and an explicit statement of what was and was not read.
