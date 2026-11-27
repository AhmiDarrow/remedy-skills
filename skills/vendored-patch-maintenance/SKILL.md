---
name: vendored-patch-maintenance
version: 1.0.0
description: >
  Carry a local fix to a third-party dependency as a tracked patch that survives upgrades. Use when you must modify vendored or installed library code before upstream releases a fix.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - dependencies
  - patching
  - build
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - grep
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: vendored-patch-maintenance
  official: true
  domain: tooling
  security_flags: []
---

# Vendored Patch Maintenance

## When to use
A dependency has a bug that blocks you and no released version fixes it.
## Steps
1. Reproduce the bug against the exact version in use with a minimal test.
2. Search upstream issues and commits. If a fix exists, backport that commit instead of inventing one.
3. Check the license permits modification and note any notice requirements.
4. Never edit the installed package directory and leave it there. Choose the ecosystem's durable mechanism: pnpm or Yarn patch commands, patch-package, Cargo `[patch]`, a Go `replace` directive, a `.patch` applied by the build, or a fork pinned to a full commit SHA.
5. Keep the patch minimal, with no formatting changes.
6. Record beside it: reason, upstream link, base version, and the condition for removal.
7. Keep your reproducing test in your own test suite so it checks the behavior, patched or not.
8. Make patch application fail the build when it does not apply cleanly; verify by installing from an empty cache and in the production image.
9. Draft the upstream report or contribution, and ask the user before submitting it.
10. On each upgrade, first try without the patch and run the test.
## Watch out for
- Packages shipping compiled output need the shipped file patched, not only the source.
- Go `replace` and similar directives in a library are not applied for its consumers.
- Branch references in forks drift; pin commits.
- Long-lived forks miss security fixes; set a review date.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean install applies the patch automatically, the reproducer passes only with it, and the removal condition is documented.
