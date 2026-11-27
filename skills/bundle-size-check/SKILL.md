---
name: bundle-size-check
version: 1.0.1
description: >
  Measure a JavaScript production bundle, find what caused a size regression and verify cuts or code splits with before and after numbers. Use when pages load slowly or a size budget fails.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - perf
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: bundle-size-check
  official: true
  security_flags: []
---

# Bundle Size Check

## When to use
Shipped JavaScript or CSS grew, or first load is too heavy.

## Steps
1. Read the build scripts and bundler config. Run the production build, never the dev server.
2. Record per chunk: raw and compressed size (gzip or Brotli, matching what the server sends), and which chunks each key route loads initially. Total output size hides this.
3. For a regression, build the last good commit in a separate worktree with the same toolchain and lockfile install, then compare. File hashes differ, so match chunks by contents.
4. Generate a composition report with the bundler's stats output or an analyzer already installed, or source-map-explorer. Ask before adding a dependency.
5. In heavy chunks look for: duplicate versions of one package (check the lockfile), whole-library imports, barrel files pulling unused modules, all locales or icons, unneeded polyfills, server-only or dev-only code, large inlined assets.
6. Trace why each heavy module is included from its import chain before proposing removal.
7. Rank fixes by initial-load bytes saved: delete, import narrowly, deduplicate, load on demand at routes or rarely used features, then replace a dependency.
8. Apply one change at a time, rebuild and record the delta. Exercise each lazy path, including loading and failure states.
9. Propose a per-chunk budget check in CI using the measured baseline.

## Watch out for
- Moving code to another chunk that is still loaded at startup saves nothing.
- Many tiny lazy chunks create request waterfalls.
- Marking packages side-effect free to help tree shaking can silently drop CSS or polyfills.
- Published package size is not what your build includes after tree shaking.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A before and after table shows compressed initial-load size per key route, the cause of any regression is named, and the changed paths were exercised.
