---
name: works-here-fails-there
version: 1.0.0
description: >
  Diagnose code that works on one machine or environment and fails on another by diffing the environments. Use when a failure appears only in CI, in production or on one person's computer.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - debugging
  - environments
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
  - write
metadata:
  source: library
  library_id: works-here-fails-there
  official: true
  domain: tooling
  security_flags: []
---

# Works Here Fails There

## When to use
Same commit, different result. Something outside the diff differs, so compare worlds instead of rereading code.
## Steps
1. Prove it is the same code and artifact: commit hash on both, `git status --porcelain` clean, same build output or image digest.
2. Capture both sides with identical commands: OS and architecture, runtime versions, resolved dependency list (`pip freeze`, `npm ls`, `cargo tree`), locale, timezone, current directory, user and permissions.
3. Diff environment variable names, and values for non-secret ones. Never print secret values or anything derived from them (length, prefix, hash); compare only whether each is set, or have the user confirm they match. Do not dump the whole environment.
4. Check file system traits: case sensitivity (macOS and Windows defaults are insensitive), line endings, path length and separators, untracked or ignored files that exist only on the working machine.
5. Check data and services: schema version, record shapes, feature flags, proxy, certificates, DNS.
6. Check resources: CPU count changes thread-pool timing; memory and disk limits differ in containers.
7. Move one difference at a time from the failing side to the working side until the working side fails. That is stronger than fixing by guess.
8. Fix by declaring the requirement (lock file, pinned version, startup check with a clear message), not by hand-tuning the broken machine.
## Watch out for
- Assuming the lock file was honoured; check what actually got installed.
- Caches in CI restoring stale dependencies.
- Shell differences between interactive and service sessions, which load different PATH and variables.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
One identified difference toggles the failure on and off, and the fix makes that requirement explicit or detected.
