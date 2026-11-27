---
name: php-version-upgrade
version: 1.0.0
description: >
  Upgrade a PHP application across minor or major versions, handling deprecations, stricter types and extension changes. Use before changing the PHP runtime on a server or image.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - php
  - upgrade
  - backend
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
  - web.fetch
  - todo
metadata:
  source: library
  library_id: php-version-upgrade
  official: true
  domain: tooling
  security_flags: []
---

# Php Version Upgrade

## When to use
The running PHP release is old or a dependency needs a newer one.
## Steps
1. Record `php -v`, `php -m` and effective ini settings for both command line and web SAPI, which often differ.
2. Read the official migration guide for each version crossed, noting backward incompatible changes.
3. Run `composer check-platform-reqs` and `composer why-not php <target>` to list blocking packages.
4. Upgrade those packages on the old runtime where possible.
5. Run a static analyzer or automated refactoring tool already used by the project, configured for the target version, and review its edits in small commits.
6. Look for common breaks: PHP 8.0 changed loose comparison between numbers and non-numeric strings and made many internal functions throw `TypeError`; 8.1 deprecated passing null to non-nullable internal parameters; 8.2 deprecated dynamic properties.
7. Set `error_reporting` to include deprecations in tests and staging and collect log entries from real traffic paths, cron jobs and queue workers.
8. Build the new image or install with required extensions, then run the test suite and smoke test uploads, mail, dates, serialization and payment sandbox flows.
9. Plan rollback and restart FPM and long-running workers during deploy.
## Watch out for
- Suppressing deprecations in config just postpones the fatal errors of the following release.
- Composer's `config.platform.php` can lie about the real runtime; update it deliberately.
- Extensions removed from core or not yet built for the target can block the move.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tests and smoke checks pass on the target runtime with deprecation logging on, and remaining notices are listed with owners.
