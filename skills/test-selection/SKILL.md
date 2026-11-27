---
name: test-selection
version: 1.0.1
description: >
  Choose and run the smallest set of tests that gives real evidence for the current change, then say what was skipped. Use when the full suite is too slow for the edit loop or someone asks what to run.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - ci
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
metadata:
  source: library
  library_id: test-selection
  official: true
  security_flags: []
---

# Test Selection

## When to use
You need fast, defensible feedback on a specific change.

## Steps
1. Collect all changes: `git status --short` (including untracked), staged and unstaged diffs, and `git diff --name-only <base>...HEAD`.
2. Read the project's test commands in CI configuration and scripts.
3. Map each change to tests of the file, tests of its callers (search imports and symbol uses), and integration tests of its boundary.
4. Prefer a dependency-aware selector when configured: Jest `--findRelatedTests`, Vitest `related`, or the build tool's affected-project filter. Check its base reference and that history is deep enough.
5. Widen to a package or full run for changes that static import tracing misses: lockfiles, build or test config, shared fixtures, schema and migrations, environment, generated code, reflection, dynamic loading and data files.
6. List the selected tests and why, then run fastest first. Confirm the runner executed a nonzero, expected number; a filter matching nothing can look like success.
7. For a bug fix, confirm the new test fails without the fix.
8. Report commands, counts, failures with file and line, and what remains for the full run before merge.

## Watch out for
- Matching only by filename misses indirect callers.
- Cached results may not reflect inputs the cache key ignores.
- Follow a project or user rule about when full suites or gates run.
- A selected run must never be reported as "all tests pass".

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chosen tests ran with results shown, the reason for the selection is stated, and unrun areas are named.
