---
name: dependency-direction-guard
version: 1.0.0
description: >
  Define which layers or modules may depend on which and enforce it automatically in the build. Use when an architecture exists on paper but imports keep crossing its boundaries.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - architecture
  - enforcement
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - bash
  - write
  - edit
metadata:
  source: library
  library_id: dependency-direction-guard
  official: true
  domain: backend
  security_flags: []
---

# Dependency Direction Guard

## When to use
Domain code imports the web framework, or UI code queries the database, despite agreement that it should not.
## Steps
1. Extract the actual dependency graph between top-level modules with the language's tooling or import search.
2. Write the intended rules as allowed edges, in a handful of lines, each with the reason (what stays replaceable or testable).
3. Compare the two and list violations with file locations.
4. Pick an enforcement mechanism: package or crate boundaries the compiler respects, dependency-cruiser or lint rules for JavaScript, import-linter for Python, ArchUnit for Java, or a small test that parses imports.
5. Freeze existing violations in an explicit baseline so the check can go in now and fails only on new ones.
6. Prove the check works by adding a forbidden import temporarily and watching it fail.
7. Make the failure message state the rule and the preferred alternative.
8. Burn down the baseline by moving code or inverting dependencies, removing entries as they are fixed.
9. Put the check in the project's normal gate.
## Watch out for
- Rules so strict that people route around them through a "shared" module open to everyone.
- Wildcard exemptions in the baseline that admit new violations.
- Type-only or dynamic imports the checker does not see.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The gate fails on a new forbidden dependency, the existing exceptions are listed individually, and each rule has a stated reason.
