---
name: pr-description
version: 1.0.1
description: >
  Draft a pull request title and body from the branch's real commits and diff, with reasons, test evidence and risks. Use before opening or updating a pull request.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - pr
  - docs
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: pr-description
  official: true
  security_flags: []
---

# Pr Description

## When to use
The user wants a pull request opened, described or summarised for reviewers, or the existing description no longer matches the branch.

## Steps
1. Identify the real base branch; for stacked work it is not the default branch. Fetch it.
2. Run `git status`, `git log --oneline origin/<base>..HEAD`, `git diff --stat origin/<base>...HEAD` and read the full diff. Mention uncommitted or unpushed work that the pull request will not contain.
3. Look for a pull request template (for example under `.github/`) and recent merged requests. Follow their sections.
4. Find the reason in commit bodies, linked issues and the conversation. If it is not recorded, ask instead of inventing one.
5. Write a title naming the observable change, in the repository's title style.
6. In the body give: the problem; the approach and why it was chosen; behaviour changes a user or caller will notice; where reviewers should look closely.
7. Report testing precisely: commands actually run and their results, manual checks, and what was not tested. Do not tick boxes for checks that did not happen.
8. Add rollout notes when the diff includes migrations, configuration, new environment variables, dependency changes, flags or API breaks, including how to roll back.
9. Link issues using only ids found in the work. Closing keywords such as `Fixes #12` can close the issue on merge, so use them only for full fixes.
10. Show the draft. Create or edit it only on request, for example `gh pr create --base <base> --title <title> --body-file <file>`, then read it back with `gh pr view`.

## Watch out for
- Narrating commit by commit, including work later reverted, instead of describing the final diff.
- Pasting logs or screenshots containing tokens or personal data.
- Overwriting reviewer-edited text or checklist state when updating a description.
- A "small refactor" description hiding a behaviour change found in the diff.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every claim traces to the diff, history or a check that ran, untested areas and rollout risks are stated, and the text is ready or posted with approval.
