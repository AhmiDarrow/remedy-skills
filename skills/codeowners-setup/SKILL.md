---
name: codeowners-setup
version: 1.0.1
description: >
  Create or repair a CODEOWNERS file so review requests reach the right people and can be required by branch rules. Use when owners are missing, wrong or not being enforced.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - process
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: codeowners-setup
  official: true
  security_flags: []
---

# Codeowners Setup

## When to use
A repository needs automatic review routing, or an existing CODEOWNERS file does not behave as expected. Syntax and enforcement differ between hosts, so identify the host and check its current documentation.

## Steps
1. Find existing files. GitHub looks in `.github/`, the repository root and `docs/`, in that order, and uses the first one found.
2. Gather evidence for ownership: directory layout, `git shortlog -sn --since="1 year ago" -- <path>`, and team documents. Commit counts suggest candidates only; the user confirms owners.
3. Prefer teams over individuals. Verify each handle exists and that users or teams have write access to the repository; teams must also be visible.
4. Order from general to specific. On GitHub the last matching pattern wins for a path, and its owners replace earlier ones. To require either of two owners, put both on one line.
5. Anchor paths deliberately: `/docs/` means the root directory, while `docs/` matches that directory at any depth. `docs/*` does not cover nested files.
6. Do not rely on gitignore negation with `!`, bracket ranges or escaped leading `#`; GitHub does not support them. Paths are case-sensitive.
7. Give CODEOWNERS itself and CI workflow definitions explicit owners.
8. Test a list from `git ls-files` against the rules, report unowned critical paths and rules matching nothing, and check the host's syntax error view after pushing a branch (ask before pushing).
9. Report the branch rule setting needed to require owner approval. The file alone only requests review. Ask before changing repository settings.

## Watch out for
- A broad pattern added at the bottom overriding every specific owner.
- A nonexistent or unauthorised owner leaving a path silently unreviewed.
- A required owner group with one person who cannot approve their own change.
- Expecting a change in the pull request branch to apply immediately; GitHub uses the file on the base branch.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Critical paths resolve to confirmed owners with access, the host reports no errors, and the enforcement setting is verified or listed as pending.
