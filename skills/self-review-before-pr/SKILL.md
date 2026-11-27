---
name: self-review-before-pr
version: 1.0.0
description: >
  Review your own diff as a hostile reader before asking anyone else to. Use before opening a pull request or handing a finished change to another person.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - review
  - workflow
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: self-review-before-pr
  official: true
  domain: git
  security_flags: []
---

# Self Review Before Pr

## When to use
The work feels done. Reviewers should spend time on design, not on your leftover prints.
## Steps
1. Fetch the target branch and view exactly what will be proposed: `git diff origin/main...HEAD` (three dots, from the merge base). Substitute the real base branch.
2. Check the file list first with `--stat`. Question every file you did not intend to touch, especially lock files, generated output and editor settings.
3. Check `git status` for new files the change needs that were never added.
4. Read the diff top to bottom without editing; note problems, then fix them in a second pass.
5. Hunt leftovers: debug output, commented-out code, skipped or focused tests (`.only`, `skip`), hardcoded local paths, TODOs with no ticket.
6. Scan added lines for secrets and personal data. If one was ever committed, removing it in a later commit is not enough; tell the user so it can be rotated.
7. For each behaviour change, name the test or manual check that covers it. Run the project's own gate and read the result.
8. Run `git diff --check` for whitespace errors and conflict markers.
9. Draft notes pointing the reviewer to risky spots and anything deliberately left out.
## Watch out for
- Reviewing the editor's view of files, which hides deletions and renames.
- A two-dot diff against a moved base showing other people's changes as yours.
- Fixing findings and not rerunning the checks afterwards.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The diff contains only intended changes, no leftovers or secrets remain, and the project checks passed on the final commit.
