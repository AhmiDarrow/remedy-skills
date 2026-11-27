---
name: codemod-write-and-apply
version: 1.0.0
description: >
  Write and run a syntax-aware codemod that changes a code pattern across many call sites. Use when an API's call shape changes and text search-and-replace or editor rename cannot express it.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - refactoring
  - codemod
  - automation
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - write
  - bash
metadata:
  source: library
  library_id: codemod-write-and-apply
  official: true
  domain: tooling
  security_flags: []
---

# Codemod Write And Apply

## When to use
Hundreds of sites need a structural change, such as reordering arguments or turning positional parameters into an options object. For a plain rename of a name or term, this is more than you need.
## Steps
1. Start from a clean branch so the mechanical rewrite can be reviewed and reverted as one diff.
2. Inventory with `grep` and sample the variants: multi-line calls, aliased and re-exported imports, spread arguments, wrappers, and generated or vendored files to exclude.
3. Use the syntax-aware tool that fits the language and project (jscodeshift, LibCST, ast-grep, OpenRewrite, clang tooling); check the installed version's API.
4. Write input and expected-output fixtures first, including lookalike code that must stay unchanged.
5. Match on the binding being the target (its import or type), not just the function name.
6. Where intent cannot be inferred, report the site with file and line instead of guessing.
7. Dry run, then compare changed and skipped counts with the inventory.
8. Apply, run the codemod again and confirm it produces no diff.
9. Search for dynamic uses it cannot see (reflection, string keys, docs), then format, build and test. Keep manual follow-ups in a separate commit.
## Watch out for
- A transform that is not idempotent wraps already converted calls a second time.
- Some printers drop comments or reformat whole files; check the diff early.
- Reordering arguments can change evaluation order when they have side effects.
- Parse failures may skip files with only a log line; count them.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Fixtures pass, every inventoried site is converted or listed as manual, a second run changes nothing, and build and tests pass.
