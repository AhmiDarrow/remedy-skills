---
name: zfs-pool-maintenance
version: 1.0.0
description: >
  Maintain a ZFS pool through health checks, scrubs, snapshot control and correct disk replacement or expansion. Use when a pool is degraded, nearly full or has not been scrubbed.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - zfs
  - storage
kind: native
status: discovered
tools:
  - bash
  - read
  - routines.create
  - owner.notify
metadata:
  source: library
  library_id: zfs-pool-maintenance
  official: true
  domain: ops
  security_flags: []
---

# Zfs Pool Maintenance

## When to use
You administer a ZFS pool that needs routine care or a disk replaced.

## Steps
1. Capture `zpool status -v`, `zpool list`, `zfs list -o space` and the OpenZFS version before any change.
2. Verify backups of important datasets exist outside this pool.
3. Interpret errors by column: read, write and checksum. Check cables, power, controller and SMART data before running `zpool clear`.
4. Schedule regular scrubs, commonly monthly, and notify on non-healthy state or new errors. Check whether the distribution already schedules them.
5. Watch capacity and fragmentation; performance degrades as pools get full, so plan expansion well before then.
6. For space, list snapshots by used and referenced size. Preview destruction with `zfs destroy -nv`; holds and replication bases must be kept.
7. To replace a disk, map the failed vdev to a physical serial, use stable `/dev/disk/by-id` paths and run `zpool replace <pool> <old> <new>`.
8. Wait for resilver to finish before touching another disk. On boot pools, also copy partition layout and bootloader as the platform documents.
9. To expand, decide between adding a vdev, replacing every member with larger disks, or version-supported RAIDZ expansion. Preview with `zpool add -n`.
10. Test email or notification delivery from the event daemon.

## Watch out for
- `zpool add` creates a new top-level vdev; adding a single disk by mistake leaves that part without redundancy and may be impossible to undo. Mirroring an existing disk is `zpool attach`.
- Snapshots share the pool's fate.
- Do not use `-f` to silence a warning you have not understood.
- `zpool upgrade` can prevent import by older systems or boot loaders.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The pool reports healthy with no unexplained errors after a completed scrub or resilver, and scheduled scrubs and alerts are verified.
