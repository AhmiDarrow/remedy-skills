---
name: linux-patching-routine
version: 1.0.0
description: >
  Set up safe recurring OS patching with preview, automatic security updates, reboot and service-restart detection and staged rollout. Use when servers are patched irregularly or never rebooted.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - linux
  - maintenance
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - routines.create
  - owner.notify
metadata:
  source: library
  library_id: linux-patching-routine
  official: true
  domain: ops
  security_flags: []
---

# Linux Patching Routine

## When to use
One or many Linux hosts need a dependable update process.

## Steps
1. Record each host's distribution, version, end-of-support date, role and acceptable downtime. An unsupported release needs an upgrade plan; patching cannot fix it.
2. List third-party repositories, held packages and manually installed software that the package manager will not update.
3. Preview pending updates (`apt list --upgradable` after `apt update`, or `dnf check-update`) and read what will be removed, not just upgraded.
4. Decide what is automatic: usually security updates through `unattended-upgrades` or `dnf-automatic`. Hold databases, cluster members and similar for planned windows.
5. Order the rollout: test host, low-risk hosts, then the rest, never all members of a redundant set at once.
6. Before kernel or major service updates, verify backups and console access, and check free space in `/boot`.
7. After updating, detect stale processes with `needrestart` or `needs-restarting`; on Debian-family systems also check `/var/run/reboot-required`.
8. After reboot, compare running kernel, failed units, listening ports and application health with the pre-update record.
9. Report hosts that failed, are pending reboot or stopped reporting.

## Watch out for
- An installed patch does not protect a process still using the old library.
- Automatic updates fail silently on lock files, expired repository keys or full disks.
- Blindly accepting package config prompts can overwrite local settings.
- Containers and language packages need separate updating.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each host has a stated policy and window, a full cycle has run including a verified reboot, and failures produce a notification.
