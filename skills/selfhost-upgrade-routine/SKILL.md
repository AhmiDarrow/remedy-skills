---
name: selfhost-upgrade-routine
version: 1.0.0
description: >
  Upgrade self-hosted applications safely by reading release notes, backing up app and database together, and planning real rollback. Use before updating containers or packages that hold your data.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - selfhost
  - maintenance
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - web.fetch
metadata:
  source: library
  library_id: selfhost-upgrade-routine
  official: true
  domain: ops
  security_flags: []
---

# Selfhost Upgrade Routine

## When to use
A self-hosted app is behind, especially by several versions.

## Steps
1. Record the running version and image digest, not just the tag, plus database and plugin versions.
2. Read every release note between current and target. Find breaking changes, required intermediate versions, config renames and database major upgrades.
3. Plan hops in the order the project requires.
4. Take a consistent backup of database, files and config at the same point, stopping writers if needed. Confirm the dump is readable and the free space sufficient for migration.
5. For important apps, restore that backup to an isolated copy and upgrade it first. Disable its outgoing email, webhooks and scheduled jobs.
6. Update the pinned version in the version-controlled file and show the diff.
7. Pull before stopping, then recreate and follow logs until migrations finish. Do not interrupt them.
8. Verify login, core actions, background jobs, integrations and clients such as mobile apps.
9. If it fails, restore old version together with old data; many migrations cannot run against older code.
10. Keep the backup for an agreed period and then upgrade the next app, one at a time.

## Watch out for
- Changing a database image's major version on an existing data directory usually fails to start; use dump and restore or the documented upgrade tool.
- A health check turning green can precede background migrations finishing.
- Pruning old images immediately removes the quickest rollback.
- Users writing data between backup and rollback will lose it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The target version passes functional checks, logs show migrations complete, and the rollback material is retained and labelled.
