---
name: dead-code-removal
version: 1.0.0
description: >
  Find unused code, prove it is unreachable and delete it safely in reviewable pieces. Use when a codebase carries unused functions, files, exports or branches that confuse readers.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - refactoring
  - cleanup
kind: native
status: discovered
tools:
  - grep
  - glob
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: dead-code-removal
  official: true
  domain: tooling
  security_flags: []
---

# Dead Code Removal

## When to use
Code looks abandoned. "Looks" is not proof.
## Steps
1. Gather candidates with a tool suited to the language (compiler unused warnings, `knip` for TypeScript, `vulture` for Python, `deadcode` from golang.org/x/tools for Go). Treat output as leads.
2. List the real roots: entry points, exported library API, framework conventions, build scripts, tests, plugins.
3. For each candidate, search for its name as a string too, covering reflection, templates, config, SQL and serialised class names.
4. Check conditional compilation and platform branches: unused on this OS may be live on another.
5. Check history with `git log -S name` to see whether it is half-built new work, not leftovers. Ask the owner if recent.
6. Where doubt remains and the system runs in production, add a usage counter or log and wait through a full usage cycle, including monthly jobs.
7. Delete in themed commits, including tests that only exercise the dead code, then orphaned dependencies, config and assets.
8. Rerun the tool, since removal exposes more dead code. Build all targets.
## Watch out for
- Test-only references making dead production code look alive.
- Rarely used recovery paths (restore, downgrade, migration from old versions) that seem unused until the day they matter.
- Commenting code out instead of deleting; history already keeps it.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each removal has recorded evidence of no reachable use, all build targets and checks pass, and orphaned dependencies are gone.
