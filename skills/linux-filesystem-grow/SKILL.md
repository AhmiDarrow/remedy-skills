---
name: linux-filesystem-grow
version: 1.0.0
description: >
  Expand a Linux disk, partition, LVM volume and filesystem in the right order with snapshots and verification. Use when a server or VM volume was enlarged or needs more space.
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
metadata:
  source: library
  library_id: linux-filesystem-grow
  official: true
  domain: ops
  security_flags: []
---

# Linux Filesystem Grow

## When to use
More capacity must reach a mounted filesystem without losing data.

## Steps
1. Map the whole stack with `lsblk -f`, `findmnt`, `pvs`, `vgs`, `lvs` and `mdstat` if present: disk, partition, RAID, encryption, LVM, filesystem.
2. Verify a recent restorable backup or take a snapshot at the VM or storage layer. Save the partition table with `sfdisk -d`.
3. Confirm the kernel sees the new size; rescan the device or reboot if not.
4. Grow each layer from the bottom up, skipping those absent.
5. Partition: `growpart /dev/sda 3` takes the disk and partition number as separate arguments. It only works into free space directly after that partition.
6. RAID if present, then encryption with `cryptsetup resize`.
7. LVM: `pvresize` the device, then `lvextend` the intended volume; `-r` also resizes the filesystem. Consider leaving free extents in the volume group.
8. Filesystem if not already done: `resize2fs <device>` for ext4, `xfs_growfs <mountpoint>` for XFS, `btrfs filesystem resize max <mountpoint>` for Btrfs.
9. Verify with `df -h` and `lsblk`, check kernel logs, and confirm applications still write.

## Watch out for
- XFS cannot be shrunk, so do not over-allocate on the assumption you can take it back.
- Device names change between boots; confirm by size, serial and mount before each command.
- `pvcreate` or `mkfs` on a device already holding data destroys it. Growing never needs `mkfs`.
- A swap or recovery partition placed after the target blocks growth; moving it is a separate, riskier job.
- Adding a second disk to a volume group makes the volume depend on both disks.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The target mount shows the new capacity, other filesystems are unchanged and no storage errors appear.
