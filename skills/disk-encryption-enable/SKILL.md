---
name: disk-encryption-enable
version: 1.0.0
description: >
  Enable full-disk encryption on Windows, macOS or Linux safely, securing recovery keys before encryption and verifying afterwards. Use when a laptop or drive with private data is unencrypted or its recovery is unknown.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - encryption
  - privacy
kind: native
status: discovered
tools:
  - bash
  - read
  - web.fetch
  - owner.notify
metadata:
  source: library
  library_id: disk-encryption-enable
  official: true
  domain: security
  security_flags: []
---

# Disk Encryption Enable

## When to use
Data should be unreadable if a device or disk is lost or stolen.

## Steps
1. Check current state: `manage-bde -status` on Windows, `fdesetup status` on macOS, `lsblk -f` on Linux. It may already be on, or suspended.
2. Take and verify a backup. Check disk health and have the machine on mains power.
3. Choose the native option: BitLocker or device encryption, FileVault, or LUKS. On Windows, check what the edition supports.
4. Decide where the recovery key will live: somewhere off this device that survives its loss, such as a password manager or printed copy in a safe place. The user views and stores it; do not read it into chat or files.
5. For organisations, set up escrow before enabling.
6. Understand unlock: TPM only, TPM with PIN, or passphrase. A higher-theft or sensitive profile favours pre-boot authentication.
7. On existing Linux installs, in-place encryption is risky; a reinstall onto LUKS and restore is usually safer. Check that swap and hibernation are covered.
8. Enable, wait for completion and confirm status shows protection on.
9. Have the user verify the saved key matches the volume's key identifier. For LUKS, keep a second keyslot and a header backup (`cryptsetup luksHeaderBackup`) stored securely off the disk.
10. Cover external and backup drives too.

## Watch out for
- Losing all keys means losing the data permanently.
- A recovery key saved on the encrypted disk is useless.
- Firmware updates or boot changes can trigger recovery prompts.
- An old LUKS header backup still accepts passphrases that were later removed.
- Encryption does not protect a running, unlocked computer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every in-scope volume reports encryption active, the user has confirmed an off-device recovery method, and a reboot unlocks normally.
