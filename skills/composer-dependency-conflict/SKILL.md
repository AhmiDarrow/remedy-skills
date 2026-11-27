---
name: composer-dependency-conflict
version: 1.0.0
description: >
  Solve Composer resolution failures in PHP projects and update packages without unrelated churn. Use when composer require or update says requirements cannot be resolved.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - php
  - composer
  - dependencies
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
metadata:
  source: library
  library_id: composer-dependency-conflict
  official: true
  domain: tooling
  security_flags: []
---

# Composer Dependency Conflict

## When to use
Composer refuses to install or upgrade a package.
## Steps
1. Read the "Problem 1" chain from the top; it ends at the incompatible constraint.
2. Confirm the environment with `composer diagnose` and `composer check-platform-reqs`. A missing `ext-*` is an environment problem, not a version problem.
3. Ask Composer directly: `composer why-not vendor/package 3.0.0` and `composer why vendor/other`.
4. List candidates with `composer show vendor/package --all`.
5. Do a trial with `composer require vendor/package:^3.0 --dry-run -W`, where `-W` allows its dependencies, including locked ones, to move.
6. If the blocker is your own root constraint, change it. If it is a third package, upgrade or replace that one.
7. Update only what you intend: `composer update vendor/package --with-dependencies`.
8. Check `minimum-stability` and `prefer-stable` before accepting dev versions; a per-package stability flag is narrower than lowering the global one.
9. Review the `composer.lock` diff and run `composer validate`, tests and `composer audit`.
10. Commit `composer.json` and the lock together; deploy with `composer install`, never update.
## Watch out for
- `--ignore-platform-reqs` produces a vendor tree that can fatal in production.
- A bare `composer update` upgrades everything.
- Plugins and post-install scripts execute code; review newly requested plugin allowances before accepting.
- Lock hash warnings mean the JSON changed without a lock update; do not hand-edit the hash.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
`composer install` succeeds from the committed lock on the target PHP version, and the lock diff holds only explained changes.
