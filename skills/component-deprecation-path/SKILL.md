---
name: component-deprecation-path
version: 1.0.0
description: >
  Replace or remove a design-system or shared UI component without breaking consumers, using usage data and codemods. Use when retiring a component, prop or token that other teams use.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - design-system
  - migration
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: component-deprecation-path
  official: true
  domain: frontend
  security_flags: []
---

# Component Deprecation Path

## When to use
A new component supersedes an old one, or a breaking change to a shared API is needed.

## Steps
1. Measure usage across all consuming repositories you can access: imports, props and variants used, wrapper components and CSS that targets internal class names. State which consumers you cannot see.
2. Compare old and new behaviour, including keyboard, focus, events, form participation, layout footprint and test hooks. Close gaps or document them.
3. Write a mapping table from old usage to new, marking cases that need human judgement.
4. Ship the replacement first and prove it on a real screen.
5. Mark the old API deprecated with type annotations, a one-time development warning that names the replacement, and documentation.
6. Write a codemod for the mechanical cases. It should leave a clear marker where it cannot decide. Dry-run it and review the diff.
7. Block new usage with a lint rule, keeping an explicit allowlist of existing files that only shrinks.
8. Migrate in reviewable slices with visual comparison.
9. Announce the removal version in the changelog and remove it only in a release the versioning policy allows, after the count reaches zero or owners accept the break.

## Watch out for
- Text search misses re-exports, aliases and dynamic imports.
- Consumers depending on DOM structure or class names break even when props are unchanged.
- A warning without a replacement and date is ignored indefinitely.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Known usage is zero or each remainder has an owner's acceptance, new usage fails lint, and the removal is recorded under the correct version with migration notes.
