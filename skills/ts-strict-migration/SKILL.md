---
name: ts-strict-migration
version: 1.0.1
description: >
  Enable TypeScript strict checks in stages without freezing development or hiding errors behind any. Use when a codebase compiles with strict off and needs tightening safely.
author: Remedy Official
license: Apache-2.0
tags:
  - typescript
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: ts-strict-migration
  official: true
  security_flags: []
---

# Ts Strict Migration

## When to use
An existing project needs stricter type checking.

## Steps
1. Record compiler version, effective config (`tsc --showConfig`), all tsconfig projects and the real type-check command. Many bundlers and transpilers strip types without checking them.
2. For each flag under `strict`, trial it with `--noEmit` and count errors. The set and defaults depend on version, so check the compiler docs: from TypeScript 6.0 `strict` is on unless set to false, and `alwaysStrict: false` is deprecated, so check the effective settings before and after any compiler upgrade.
3. Order the work: low-error flags such as `noImplicitThis` or `alwaysStrict` first; then `noImplicitAny`; then `strictNullChecks`, usually the largest. Options like `noUncheckedIndexedAccess` sit outside `strict` and are a separate decision.
4. For large codebases, ratchet by project references, a stricter config listing cleaned files, or an error baseline that CI only lets shrink. Remember imported files are checked under that config too.
5. Fix from shared types and boundaries outward. Use `unknown` plus real validation or narrowing for external data.
6. Model absence honestly. When a `null` case is reached, decide the correct behaviour and test it.
7. Allow a temporary suppression only with a reason and tracking; prefer `@ts-expect-error`, which reports when it is no longer needed.
8. After each stage run type check and tests, enable the flag in CI, and commit before the next.

## Watch out for
- Non-null `!` and `as` remove errors while keeping the crash.
- Adding defaults like empty strings or zero can silently change behaviour.
- `skipLibCheck` skips checking declaration files, including your own `.d.ts`.
- One mega-change collides with all other work.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The agreed flags are enforced in CI for the stated scope, tests pass, and remaining escapes and unchecked areas are counted and listed.
