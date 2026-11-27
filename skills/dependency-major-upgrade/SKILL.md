---
name: dependency-major-upgrade
version: 1.0.0
description: >
  Upgrade one important library across a breaking major version with a changelog-driven plan and verification. Use when a framework or core dependency is several majors behind.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - dependencies
  - upgrade
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - web.fetch
  - todo
metadata:
  source: library
  library_id: dependency-major-upgrade
  official: true
  domain: tooling
  security_flags: []
---

# Dependency Major Upgrade

## When to use
The upgrade is expected to break something, so bumping the number and running tests is not enough.
## Steps
1. Record the installed version from the lock file, and the target's requirements for language, runtime and peers.
2. Fetch the official changelog and migration guide for every major crossed. Extract breaking items into a list.
3. For each item, `grep` the codebase and mark it affected (with sites), not affected, or unknown. Include configuration files and string-based usage.
4. Check that plugins and wrappers around the library support the target.
5. Establish a green baseline, and add characterization tests around affected behavior that currently has none.
6. If the library offers a bridge release with deprecation warnings, upgrade to it first and clear the warnings.
7. Step one major at a time when migration tools are written that way. Run official codemods and review their diffs.
8. After each step, build, test and run the real application path. Compare behavior that changes silently: defaults, serialization, timeouts, error types and ordering.
9. Check the lock diff for unexpected transitive jumps.
10. State how to roll back, especially if the new version writes data, caches or cookies the old one cannot read.
## Watch out for
- Release notes for minor versions can contain behavior changes too; skim those between your start and the bridge.
- Mocks of the library keep passing against an API that no longer exists. Run at least one test against the real thing.
- Mixing refactors into the upgrade makes regressions hard to attribute.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every breaking item has a recorded verdict, tests and a real run pass on the target, and rollback limits are stated.
