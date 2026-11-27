---
name: prose-lint-setup
version: 1.0.0
description: >
  Add automated prose and Markdown linting to a documentation repository without drowning writers in noise. Use when style comments dominate doc reviews.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - tooling
  - linting
kind: native
status: discovered
tools:
  - read
  - glob
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: prose-lint-setup
  official: true
  domain: docs
  security_flags: []
---

# Prose Lint Setup

## When to use
Reviewers keep correcting the same wording and formatting issues by hand.

## Steps
1. Collect the last several rounds of doc review comments and separate the mechanical ones; only those can be linted.
2. Check for existing configs before adding anything. Common open tools are Vale for prose rules, markdownlint for structure and a link checker.
3. Check each tool's installed version and docs for config format; do not write rule files from memory.
4. Start with a few rules: banned terms, product capitalisation, heading levels, broken relative links.
5. Add a project vocabulary file so domain words pass spelling checks.
6. Run on the whole repository and count hits per rule. Disable or downgrade rules with many false positives.
7. Make CI fail only on error-level rules, and consider checking just changed files until the backlog is cleared.
8. Document the local command and how to suppress one line with a reason.

## Watch out for
- Enabling a large third-party style pack as errors on day one.
- Bulk auto-fixing that alters code blocks or front matter.
- External link checks that fail builds because a remote site rate-limits; run them separately on a schedule.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The local command and CI give the same result, the baseline passes, and a deliberately introduced violation fails.
