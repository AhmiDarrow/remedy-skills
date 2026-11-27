---
name: docs-staleness-audit
version: 1.0.0
description: >
  Find documentation that no longer matches the code: dead commands, renamed options and removed features. Use after large refactors or when readers report wrong instructions.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - maintenance
  - audit
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
  - write
metadata:
  source: library
  library_id: docs-staleness-audit
  official: true
  domain: docs
  security_flags: []
---

# Docs Staleness Audit

## When to use
The code has moved faster than its docs and nobody knows which pages are wrong.

## Steps
1. List doc files with `glob`, including comments in example configs and templates.
2. Extract verifiable references: file paths, commands, flags, environment variables, config keys, endpoint paths, function names, version numbers.
3. Check each against the source with `grep`. For commands, compare with current `--help` output.
4. Use history to aim effort: `git log --diff-filter=DR --name-status` shows deleted and renamed files; search docs for the old names.
5. Check the reverse direction: new flags or config keys in code that no page mentions.
6. Classify each finding as wrong (will mislead), missing, or cosmetic. Record the doc line and the code evidence.
7. Fix the wrong ones first. Delete pages for removed features and leave a pointer if external links may exist.
8. Suggest one automated guard for the most frequent drift, such as testing examples in CI.

## Watch out for
- Calling a reference dead because a plain search missed a dynamically built name.
- "Updating" docs to describe a bug as intended behaviour; report it instead.
- Changing historical release notes, which correctly describe the past.
- Trusting a page's last-edited date as evidence of accuracy.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every extracted reference is marked verified, fixed or reported, with code evidence for each change.
