---
name: linux-disk-full-recovery
version: 1.0.0
description: >
  Recover a full Linux filesystem, covering inode exhaustion and deleted-but-open files, without deleting data blindly. Use when writes fail with No space left on device.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - linux
  - storage
kind: native
status: discovered
tools:
  - bash
  - read
  - owner.notify
metadata:
  source: library
  library_id: linux-disk-full-recovery
  official: true
  domain: ops
  security_flags: []
---

# Linux Disk Full Recovery

## When to use
A filesystem is full or nearly full and services are failing.

## Steps
1. Run `df -h` and `df -i`, and identify the mount behind the failing path. Free inodes can run out while bytes remain.
2. Find large trees on that filesystem only: `du -xh --max-depth=1 <mount> | sort -h`, then descend.
3. If `du` totals far less than `df`, run `lsof +L1` for deleted files still held open. Restarting or signalling the owning process frees them.
4. Also consider data hidden under a mount point, snapshots, and filesystem reserved blocks.
5. For inode exhaustion, find directories with huge file counts, such as session, mail queue or cache folders.
6. Free safe space first: `journalctl --vacuum-size=500M`, the package manager's cache clean, and already rotated logs.
7. For an active huge log, copy what is needed elsewhere, then truncate in place with `truncate -s 0`.
8. Before removing anything else, show the owner path, size, age and what writes it. Never delete database data or transaction log files by hand.
9. Fix the source: rotation, retention, a runaway debug flag, or grow the volume. Add alerts on both space and inodes.

## Watch out for
- Deleting an open log removes the name but frees nothing.
- Old kernels should be removed through the package manager, keeping the running one and a fallback; a full `/boot` also breaks upgrades.
- A service that hit a full disk may have corrupt or half-written files and need verification after restart.
- Running `du` without `-x` wanders into network mounts.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Space and inode use are safely below alert level, affected services pass a write test, and the growth source is limited or reported.
