---
name: tsc-build-time-reduction
version: 1.0.0
description: >
  Cut slow TypeScript type-check and editor response times using compiler diagnostics. Use when tsc takes minutes or the language server lags or runs out of memory.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - typescript
  - performance
  - build
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
metadata:
  source: library
  library_id: tsc-build-time-reduction
  official: true
  domain: tooling
  security_flags: []
---

# Tsc Build Time Reduction

## When to use
Type checking has become the slow step, measured rather than assumed.
## Steps
1. Baseline with `tsc --noEmit --extendedDiagnostics`. Record check time, files, types, instantiations and memory. Run it twice to separate cold and warm numbers.
2. See what is being compiled with `tsc --listFilesOnly` or `--explainFiles`. Look for build output, vendored folders, stories or unrelated `@types` packages pulled in.
3. Tighten `include` and `exclude`, and set the `types` compiler option to the global type packages actually needed.
4. If check time dominates, run `tsc --generateTrace tracedir --noEmit` and analyze the trace to find the files and types that take longest.
5. Typical fixes: give exported functions explicit return types, replace large intersections with interfaces that extend, break huge unions into narrower ones, and cut recursive conditional types.
6. Enable `incremental`, and for multi-package repos use project references with `composite` and `tsc -b`.
7. Consider `skipLibCheck`, stating that it also skips your own declaration files.
8. Separate transpiling from checking: a fast transpiler for dev builds with `isolatedModules` on, and full `tsc` in CI.
9. Rerun the baseline command after each single change and keep only changes that moved the number.
## Watch out for
- Excluding a file does not remove it if another file imports it.
- Removing the type-check step for speed lets type errors ship; confirm CI still runs it.
- Path aliases that point at package sources instead of built declarations make every consumer re-check everything.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A before and after table of diagnostics shows the improvement, and CI still fails on an intentionally introduced type error.
