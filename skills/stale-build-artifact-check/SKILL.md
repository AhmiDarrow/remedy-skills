---
name: stale-build-artifact-check
version: 1.0.0
description: >
  Confirm the code you are testing is the code you edited, ruling out stale builds, caches and wrong binaries. Use when changes seem to have no effect or behaviour contradicts the source.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - debugging
  - build
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
metadata:
  source: library
  library_id: stale-build-artifact-check
  official: true
  domain: tooling
  security_flags: []
---

# Stale Build Artifact Check

## When to use
You fixed it and nothing changed, or a line you deleted still appears to run. Check this before theorising further.
## Steps
1. Plant an unmistakable marker (a unique log line or version string) on the failing path, rebuild and run. If it is absent, you are not running this code.
2. Find what actually runs: `which -a name` or `where.exe name`, the process's executable path, and for interpreters the imported module's file path.
3. Look for a second copy: installed package shadowing the source tree, an old global install, a duplicate in a nested dependency, another checkout or worktree.
4. Check that the build step ran and covered the file: compare artifact timestamps, and confirm the file is included by the build config and not excluded.
5. Check running processes: a daemon, dev server or watcher started before the edit may still hold the old code.
6. Check the layers of caching relevant here: bytecode, bundler cache, container layers, browser or service worker cache, CDN.
7. Clear the narrowest suspect cache first so you learn which one lied. Use the tool's clean command; review any delete command's paths before running it, and use `git clean -ndx` as a dry run rather than deleting blind.
8. Make recurrence visible: print version and commit hash at startup, or fix the missing dependency in the build rules.
## Watch out for
- `git clean -fdx` removing ignored but precious files such as local config and databases.
- Stopping processes by name and killing someone else's; stop only the ones you started or identified by id.
- Leaving the marker in the committed code.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The marker proves the running program is built from the current source, and the reason it previously was not has been identified.
