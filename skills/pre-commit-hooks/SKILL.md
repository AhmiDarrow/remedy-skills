---
name: pre-commit-hooks
version: 1.0.1
description: >
  Set up fast, shared Git hooks for formatting, linting and secret checks, backed by the same checks in CI. Use when style or obvious errors keep reaching review.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: pre-commit-hooks
  official: true
  security_flags: []
---

# Pre Commit Hooks

## When to use
Contributors need quick local checks before a commit.

## Steps
1. Check for an existing system: `.pre-commit-config.yaml`, `.husky`, lefthook config, `git config core.hooksPath` and files in `.git/hooks`. Extend it; do not overwrite personal or existing hooks.
2. Choose the framework matching the project's ecosystem (pre-commit, Husky with lint-staged, or lefthook) and follow docs for the installed major version.
3. Reuse the project's formatter and linter configs and versions. Pin third-party hook revisions to a release tag or commit, and review their source since they run on contributors' machines.
4. Keep commit checks to seconds and scoped to staged files. Put type checks and tests in pre-push or CI unless they are fast.
5. Handle partially staged files with a tool that sets unstaged changes aside, so unchosen hunks are not committed.
6. Add a secret scanner with redacted output if approved.
7. Add the one-time install command to setup and contributor docs; a clone does not activate hooks by itself.
8. Run across all files once and keep the resulting mass reformat as a separate commit, with approval.
9. Run the same checks in CI. Test with a staged violation, a partially staged file, a deleted file and a filename with spaces on supported systems.

## Watch out for
- Hooks can be bypassed with `--no-verify`, so they are convenience, not enforcement.
- Two formatters fighting create a loop.
- Hooks fail in GUI Git clients or on Windows when PATH or shell differ.
- Autofixes must not silently stage unrelated changes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A planted violation blocks a test commit, a clean one passes quickly, unstaged work survives, and CI runs the same rules.
