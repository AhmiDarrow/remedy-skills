---
name: migration-guide-write
version: 1.0.0
description: >
  Write an upgrade guide for a release with breaking changes, from the actual diff. Use when users must change code, config or data to move to a new version.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - release
  - migration
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - write
metadata:
  source: library
  library_id: migration-guide-write
  official: true
  domain: docs
  security_flags: []
---

# Migration Guide Write

## When to use
A new version will break existing users unless they act.

## Steps
1. Fix the exact from and to versions. Compare the release tags with `git diff` and read changelog and pull request notes.
2. Inventory breaks in public surface: removed or renamed APIs, changed defaults, config keys, data formats, minimum runtime versions.
3. Hunt silent breaks, where old input still runs but behaves differently. These go at the top.
4. For each break give: who is affected, how to detect it (a search pattern or warning text), before and after snippets, and the replacement.
5. Order the procedure: backups, prerequisite upgrades, deprecation fixes possible on the old version, upgrade, data migration, verification.
6. Say whether rollback is possible and where the point of no return is.
7. Apply the guide to a sample project pinned to the old version and fix what you missed.
8. Note skipped-version paths: whether users may jump or must step through.

## Watch out for
- Pasting the changelog and calling it a guide.
- Detection patterns that miss aliased imports or generated config; say what they cannot catch.
- A data migration with no restore instructions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each breaking change has detection plus before and after, rollback limits are stated, and the sample upgrade succeeded or its gaps are declared.
