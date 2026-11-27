---
name: split-god-module
version: 1.0.0
description: >
  Break an oversized file or class into cohesive modules in small behaviour-preserving moves. Use when one module changes for many unrelated reasons and everything imports it.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - refactoring
  - architecture
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - bash
metadata:
  source: library
  library_id: split-god-module
  official: true
  domain: backend
  security_flags: []
---

# Split God Module

## When to use
A file has become the place where everything goes, and each edit risks unrelated features.
## Steps
1. Build a map: list each function and field, which fields each function uses, and who imports what from outside.
2. Find clusters that share data and change together. `git log -p` on the file helps show which parts move in the same commits.
3. Name each cluster by its responsibility. A cluster you can only call "utils" or "helpers" is not cohesive yet.
4. Extract the leaf first: the cluster that depends on the others least.
5. Move code verbatim in one commit with no edits beyond imports and visibility. Review with `git diff --color-moved`.
6. Keep the old module re-exporting moved names so callers keep working, then migrate callers in later commits.
7. Where clusters share mutable state, give it one owner and pass it or expose operations; do not let both new modules write it.
8. Run tests after every move. Check for import-time side effects and registration order that the split may alter.
9. Remove the temporary re-exports once no caller uses them, unless they are public API.
## Watch out for
- Mixing renames and logic fixes into move commits.
- Splitting by technical kind (all types, all constants) so every feature still touches every file.
- Reflection, mocks or serialised class paths that refer to the old module name.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each new module has a nameable responsibility, no cycle was introduced, and behaviour checks pass after each move commit.
