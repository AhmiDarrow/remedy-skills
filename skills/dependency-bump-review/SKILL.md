---
name: dependency-bump-review
version: 1.0.0
description: >
  Review a dependency version upgrade by reading what changed and what it can break in this codebase. Use when an automated or manual pull request raises a library or tool version.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - review
  - dependencies
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - web.fetch
  - web.search
metadata:
  source: library
  library_id: dependency-bump-review
  official: true
  domain: tooling
  security_flags: []
---

# Dependency Bump Review

## When to use
The diff is two version numbers and a lock file, which hides the real change.
## Steps
1. Note the exact old and new resolved versions from the lock file, not just the manifest range.
2. Diff the lock file for transitive packages added, removed or changed. A one-line bump can pull in many.
3. Read release notes and changelog for every version in between. Search for breaking, removed, deprecated, default and minimum version.
4. Grep this repo for each affected API, config key and CLI flag.
5. Check requirement changes: runtime or compiler version, peer dependencies, platforms, licence.
6. For packages with install scripts, new maintainers, a changed source URL or a very recent publish, read the published contents before installing, because installing runs those scripts. If anything is unexplained, hold; do not install it on a machine that has credentials.
7. Otherwise build and run the project's tests on the new lock file, then exercise the feature that uses the library, since tests may mock it.
8. Watch behaviour changes tests miss: default timeouts, serialisation format, rounding, sort order, TLS settings. Check that data written by the new version can be read by the old if rollback matters.
9. Report: merge, merge with listed edits, or hold with the reason.
## Watch out for
- Trusting a patch number to mean no behaviour change.
- Many unrelated bumps in one change, which makes a regression hard to pin down.
- Skipping the notes for intermediate versions on a long jump.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Changelog entries that touch your usage are listed with their effect, checks ran on the new lock file, and a recommendation is given.
