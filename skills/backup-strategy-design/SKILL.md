---
name: backup-strategy-design
version: 1.0.0
description: >
  Design backups from recovery targets with separate copies, ransomware-resistant retention, encryption key custody and monitoring. Use when setting up or reviewing how important data is protected.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - backups
  - security
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - routines.create
  - owner.notify
metadata:
  source: library
  library_id: backup-strategy-design
  official: true
  domain: ops
  security_flags: []
---

# Backup Strategy Design

## When to use
Data on computers, servers or a homelab needs a backup plan. Rehearsing a restore is covered by a restore drill.

## Steps
1. Inventory data by location and owner, including databases, VM disks, application config, secrets, phones and hosted services. Mark what can be recreated.
2. For each set agree how much data may be lost and how long recovery may take.
3. Keep at least three copies, on two different devices or media, one off site. At least one must be offline, immutable or append-only.
4. Make sure a compromised source machine cannot delete history: pull-based backups, an append-only repository server, or storage object lock. Keep deletion and pruning credentials elsewhere.
5. Choose consistent capture methods: database-native dumps or snapshot-aware tools, not a plain copy of live database files.
6. Pick a versioned, deduplicating, encrypted tool such as restic or Borg, or equivalent.
7. Have the user store the repository password and keys somewhere that survives losing the machine. Test that they can be retrieved.
8. Set retention long enough to reach back before slowly discovered corruption or encryption, and check storage growth.
9. Schedule jobs plus integrity checks that read actual data (for restic, `check --read-data-subset`). Alert when no successful backup has appeared within the expected window, not only on errors.
10. Restore a sample from each set to a different location and compare.

## Watch out for
- RAID, snapshots on the same pool and file sync are not backups; sync faithfully copies deletions.
- Hosted services keeping your data does not mean they can restore your mistakes.
- Pruning with a wrong filter can erase most history; preview with a dry run.
- A backup job may succeed while excluding the important path.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every data set has targets, destinations and a monitored schedule, one copy resists deletion from the source, and a sample restore succeeded.
