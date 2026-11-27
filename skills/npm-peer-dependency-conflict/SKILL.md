---
name: npm-peer-dependency-conflict
version: 1.0.0
description: >
  Resolve ERESOLVE and peer dependency conflicts in npm, pnpm or Yarn without hiding real incompatibilities. Use when an install fails or two copies of a framework get loaded.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - javascript
  - dependencies
  - npm
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - web.fetch
metadata:
  source: library
  library_id: npm-peer-dependency-conflict
  official: true
  domain: tooling
  security_flags: []
---

# Npm Peer Dependency Conflict

## When to use
Installation reports an unmet or conflicting peer range, or runtime errors point to duplicate instances.
## Steps
1. Identify the package manager from the lock file and use only that one.
2. Read the conflict as a triangle: who requires the peer, which range, and which version the root has. Write down all three.
3. Map the paths with `npm ls <pkg>` and `npm explain <pkg>` (or `pnpm why`, `yarn why`).
4. Query newer releases of the complaining package with `npm view <pkg> peerDependencies` and `npm view <pkg> versions`. A release that accepts your version is the best fix.
5. If none exists, check its changelog or issue tracker for known compatibility with your version.
6. Choose in this order: upgrade the plugin; hold back the host library; replace the plugin; force the version with `overrides` (npm, in `package.json`) or pnpm `overrides` (in `pnpm-workspace.yaml` from pnpm 11, `pnpm.overrides` in `package.json` on older releases). Yarn `resolutions` pins what gets installed but does not rewrite a declared peer range; check the installed version's docs for peer rules.
7. Scope any override to the specific parent where possible and add a comment or note saying why and when to remove it.
8. Delete nothing broad: update the lock by installing the specific package, then review the lock diff for unrelated jumps.
9. Exercise the plugin's real feature, then check `npm ls <peer>` shows a single copy.
## Watch out for
- `--legacy-peer-deps` or `--force` as a permanent setting hides every future conflict, and CI must then use the same flag to reproduce the tree.
- Deleting the lock file to make the error go away upgrades hundreds of packages at once.
- An override silences the resolver but does not make incompatible code work.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean `npm ci` (or frozen-lockfile equivalent) succeeds without force flags, and the affected feature has been run.
