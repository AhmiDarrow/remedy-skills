---
name: linux-boot-rescue
version: 1.0.0
description: >
  Recover a Linux machine that will not boot, identifying the failing stage and repairing fstab, initramfs or bootloader with minimal changes. Use when a host drops to an emergency shell or never comes up.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - linux
  - recovery
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: linux-boot-rescue
  official: true
  domain: ops
  security_flags: []
---

# Linux Boot Rescue

## When to use
Boot fails after an update, disk change or configuration edit. The user types console commands unless you have a rescue shell.

## Steps
1. Record the last screen messages and what changed. Classify: firmware finds no boot entry, GRUB prompt, kernel panic, initramfs shell, emergency mode, or booted without network or login.
2. If data matters and the disk logs I/O errors, stop and image it before repairing.
3. Try an older kernel from the boot menu.
4. For emergency mode, read `journalctl -xb`. A bad `/etc/fstab` entry is common: compare UUIDs with `blkid`, fix or comment the line, and add `nofail` to non-essential mounts.
5. To get further in, edit the boot entry once and add `systemd.unit=rescue.target` or `emergency.target`.
6. Otherwise boot matching live media. Identify disks with `lsblk -f`, unlock encryption, activate RAID or LVM, and mount root, then `/boot` and the EFI partition.
7. Bind-mount `/dev`, `/proc`, `/sys` and `/run`, then chroot.
8. Fix only the failing stage with the distribution's own tools: rebuild the initramfs (`update-initramfs`, `dracut` or `mkinitcpio`) or reinstall the bootloader in the same UEFI or BIOS mode as installed.
9. Check `findmnt --verify`, unmount cleanly, reboot and read the journal for remaining errors.

## Watch out for
- Running `fsck` on a mounted filesystem can destroy it; match the tool to the filesystem type.
- XFS log zeroing and similar forced repairs discard data and are a last resort.
- Booting live media in the wrong firmware mode installs the wrong bootloader.
- Never format or repartition to "fix" boot.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The machine boots unaided twice, the failed stage and cause are recorded, and no failed units relate to the repair.
