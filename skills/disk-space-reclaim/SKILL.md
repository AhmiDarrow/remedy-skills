---
name: disk-space-reclaim
version: 1.0.0
description: >
  Find what is filling a personal computer's drive and free space without breaking applications or losing data. Use when the disk is full or nearly full.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - desktop
  - storage
kind: native
status: discovered
tools:
  - bash
  - jobs
  - glob
  - owner.notify
metadata:
  source: library
  library_id: disk-space-reclaim
  official: true
  domain: tooling
  security_flags: []
---

# Disk Space Reclaim

## When to use
Low disk space is blocking updates, downloads or work.

## Steps
1. Record free and total space per volume and how much the user needs.
2. Measure before deleting: size top-level folders, then drill into the largest. Use the OS storage view, `du -h` on Unix-like systems or a PowerShell size summary on Windows.
3. Note permission-denied areas so the unexplained remainder is visible.
4. Classify big items: user files, application data, caches that rebuild, trash, old installers, virtual machine images, local model or game libraries, package caches, backups, system files.
5. For each candidate give size, what it is, what breaks or must be re-downloaded, and how it is recovered.
6. Prefer the owning tool's cleanup command or settings over deleting its folders by hand.
7. Offer moving cold data to another drive, verifying the copy before removing the source.
8. Get approval item by item or group by group, then execute exactly that.
9. Measure free space again and report the gain.

## Watch out for
- Do not hand-delete inside operating system directories, application bundles or database folders.
- Snapshots, shadow copies and trash can keep space occupied after deletion.
- Containers and virtual disks may not shrink on the host without a compaction step.
- "Cache" in a folder name does not guarantee disposable content.
- Emptying the trash is permanent and needs its own confirmation.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Free space is re-measured, every removal was approved and logged, and remaining large consumers are listed.
