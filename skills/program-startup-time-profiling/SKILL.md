---
name: program-startup-time-profiling
version: 1.0.0
description: >
  Reduce how long a command line tool, service or desktop program takes to become ready. Use when startup feels slow, cold starts breach limits, or a CLI lags before doing anything.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - profiling
  - performance
  - startup
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: program-startup-time-profiling
  official: true
  domain: tooling
  security_flags: []
---

# Program Startup Time Profiling

## When to use
Time to first useful output or to readiness is the problem.
## Steps
1. Define the finish line precisely: help text printed, first window drawn or health check passing.
2. Measure many runs with a tool such as `hyperfine` or a loop, reporting median and spread. Keep cold (after reboot or fresh container) and warm figures separate.
3. Split the time: process creation and dynamic loading, runtime startup, module imports and static initializers, then your initialization.
4. Use the runtime's own view: `python -X importtime`, Node `--cpu-prof`, JVM class loading logs, .NET event tracing, or `LD_DEBUG=statistics` for the Linux loader.
5. Trace file and network access during startup. Look for searching many paths, scanning directories, update checks and synchronous remote config.
6. Defer what the common path does not need: lazy imports for subcommands, on-demand plugin loading and later connection setup.
7. Parallelize independent initialization only after removing unnecessary work.
8. Consider ahead-of-time or precompiled options for the runtime if loading dominates, noting their compatibility limits.
9. Add a startup benchmark or imported-module check so regressions show.
## Watch out for
- The second run benefits from OS file cache and flatters the result.
- Antivirus scanning of freshly built binaries distorts Windows timings; note it, do not disable protection.
- Lazy loading moves cost and errors to first use; make sure configuration errors still surface early where needed.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Median cold and warm times are recorded before and after with the same method, and each kept change shows a measurable gain.
