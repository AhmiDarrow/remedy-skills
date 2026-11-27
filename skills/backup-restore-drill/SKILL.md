---
name: backup-restore-drill
version: 1.0.1
description: >
  Rehearse restoring a backup into an isolated target, verify the data works and measure real recovery time and loss. Use when backups have never been tested or a drill is due.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - reliability
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: backup-restore-drill
  official: true
  security_flags: []
---

# Backup Restore Drill

## When to use
There are backups and someone needs proof they can be restored. Choosing a backup design is a separate task.

## Steps
1. Pick a scenario (deleted table, lost server, lost account, encrypted data) and the target recovery time and acceptable data loss. State the pass criteria.
2. Prepare an isolated target with enough space. Block it from production databases, queues, mail, payment and webhook endpoints, and disable scheduled jobs before the application starts.
3. Present the exact restore commands with source and destination, and get approval. Check the destination host name before each command that writes. A drill never restores over production.
4. Start the clock at "incident declared". Follow only the written runbook and what would survive the scenario: can the keys, credentials, tool versions and instructions be obtained without the lost system?
5. Select the backup the scenario calls for, not always the newest. For point-in-time recovery, restore to a chosen timestamp and check the log chain is unbroken.
6. Time each phase: finding, fetching, decrypting, restoring, replaying logs, indexing, application start.
7. Verify content: integrity checks, row or file counts, newest record timestamps, sampled records, and an application smoke test. A zero exit code is not enough.
8. Compute achieved data loss from the gap between the incident time and the latest recovered record, and compare both measures with the targets.
9. List what was missing, including roles, configuration, uploaded files and secrets.
10. With approval, destroy the restored copy, then record results, fixes with owners and the next drill date.

## Watch out for
- A restored application sending real emails or charging customers.
- Production personal data landing in a less protected test environment.
- Timing a small sample and assuming recovery scales linearly.
- The one person who knows the undocumented step doing the drill.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The restored system passed or failed stated checks, measured recovery time and data loss are recorded against targets, the copy is cleaned up, and gaps have owners.
