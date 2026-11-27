---
name: dependency-audit
version: 1.0.1
description: >
  Audit a project's locked dependencies for known vulnerabilities and risky outdated packages, then plan the smallest safe upgrades. Use when checking a repository before a release or on a regular review.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - deps
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
  - edit
metadata:
  source: library
  library_id: dependency-audit
  official: true
  security_flags: []
---

# Dependency Audit

## When to use
A repository needs a whole-tree view of vulnerable, abandoned or badly outdated packages.

## Steps
1. List every lockfile and manifest, including nested packages, container images' install lines and CI tool installs. A manifest without a lockfile cannot be audited exactly; say so.
2. Run the scanner for each ecosystem if installed: `npm audit --json`, `pnpm audit`, `yarn audit` (classic) or `yarn npm audit` (newer), `pip-audit -r requirements.txt`, `cargo audit`, `govulncheck ./...`. A cross-ecosystem scanner such as `osv-scanner` reads many lockfiles; check its help because subcommands differ between versions. Install tools only with approval. Many of these send package names to a remote service, so ask first for private projects with sensitive names. `pip-audit -r` can run package code while resolving, like `pip install -r`; use it only on requirements you would install, or in an isolated environment.
3. Save raw output. Merge duplicates by advisory ID and package, counting one advisory once even if many paths pull it in.
4. For each high or critical item record installed version, fixed version, direct or transitive, runtime or development only, and the path that pulls it in (`npm ls`, `pnpm why`, `cargo tree -i`, `go mod why`).
5. Rank by exposure, not score alone: is the vulnerable function reachable, does untrusted input reach it, is it shipped. `govulncheck` reports whether code is called; most others do not.
6. Plan the least change: update within the allowed range, then bump the direct parent, then use an override or resolution with a comment and a removal condition.
7. Flag abandonment from evidence: registry deprecation notice, archived repository, or no release alongside unanswered security reports.
8. After approved changes, reinstall from the lockfile, test, and rescan.

## Watch out for
- `npm audit fix --force` can install breaking major versions, or downgrade packages.
- A development-only package still matters if it runs in CI with credentials.
- A clean scan means no known advisories, not safe code; a known malicious package needs incident response, not an upgrade.
- Ignoring a finding without a reason and review date hides it forever.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each lockfile is reported as scanned or not scanned with the reason, and every high or critical finding has an action, or a written acceptance with a review date.
