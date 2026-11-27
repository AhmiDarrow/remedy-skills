---
name: makefile-tasks
version: 1.0.1
description: >
  Add a Makefile or task-runner targets that wrap a project's real setup, test, lint, run and build commands. Use when contributors must dig through docs or CI to find how to work on a repository.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: makefile-tasks
  official: true
  security_flags: []
---

# Makefile Tasks

## When to use
Project commands are scattered or long, and one discoverable entry point would help.

## Steps
1. Gather commands from CI, README, package manifests and scripts, and run the safe ones to see which still work.
2. Reuse an existing task runner. Choose Make only if contributors have it; it is often missing on Windows, so ask who needs support and consider the language's own scripts or a cross-platform runner.
3. Define the verbs the project really has, typically help, setup, lint, test, build and run. Do not create empty ones.
4. Call the underlying tool instead of copying its configuration, and let CI use the same targets so they cannot drift.
5. In Make: recipe lines start with a tab; declare command targets `.PHONY`; each line runs in a separate shell, so join `cd` with `&&`; write `$$` for a shell dollar; use `$(MAKE)` for recursion.
6. Make `help` the default goal, with a short description per target.
7. Allow safe overrides through variables, such as a test filter. Ensure pipelines and loops propagate failures.
8. Keep destructive, deploy and publish tasks separate, clearly named and requiring an explicit environment, never prerequisites of everyday targets.
9. Run each target from a clean checkout and confirm a failing command returns nonzero.

## Watch out for
- A target named like a folder (`test`, `build`) is silently skipped unless phony.
- A leading `-` or `|| true` hides failures.
- Shell syntax and tool flags differ between GNU, BSD and Windows.
- Parallel `make -j` exposes missing prerequisites.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Listed targets run as documented on the supported systems, failures propagate, and unverified targets are named.
