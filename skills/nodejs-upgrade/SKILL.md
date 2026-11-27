---
name: nodejs-upgrade
version: 1.0.1
description: >
  Plan and carry out a Node.js runtime upgrade across local pins, CI, images, hosting and native dependencies. Use when the current Node version nears end of life or a dependency requires a newer one.
author: Remedy Official
license: Apache-2.0
tags:
  - node
  - upgrade
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - grep
  - web.fetch
metadata:
  source: library
  library_id: nodejs-upgrade
  official: true
  security_flags: []
---

# Nodejs Upgrade

## When to use
An application or library must move to a newer Node.js line.

## Steps
1. Find every pin: `engines`, `.nvmrc`, `.node-version`, tool-manager files, CI matrix, Dockerfiles, serverless runtime settings, hosting config and docs. Check what production actually runs.
2. Check the official release schedule and choose a supported LTS line; confirm the host offers it. For a published library, dropping versions is a breaking change to decide explicitly.
3. Read release notes for every major crossed. Search the code for removed or changed APIs, flags, TLS or OpenSSL behaviour, new built-in globals that clash with polyfills, and module loading changes.
4. Before switching, get a green baseline and run it with deprecation warnings traced (`--trace-deprecation`).
5. Check native addons and engine ranges for support, and package manager and `@types/node` compatibility.
6. On the target, install from the lockfile after removing built modules. Update only dependencies that block the upgrade, and explain lockfile changes.
7. Run build, types, lint and tests, then exercise startup, outbound HTTPS, streams, crypto, child processes and shutdown. Compare memory and latency under representative load.
8. Update all pins together. Roll out gradually with the old image or runtime kept for rollback.

## Watch out for
- CI on the new version while the production image stays old, or the reverse.
- Old OpenSSL errors silenced with a legacy provider flag need a real fix.
- Native binaries differ by OS, architecture and C library; test in the deployment image.
- Changed timeout, DNS ordering or unhandled rejection defaults pass unit tests and fail live.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All pins agree, checks pass on the target in the deployment environment, rollback is written down, and unverified paths are listed.
