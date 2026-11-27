---
name: windows-boot-repair
version: 1.0.0
description: >
  Repair a Windows PC that fails to boot, protecting data and BitLocker keys and treating UEFI and legacy BIOS differently. Use when Windows loops in recovery or cannot find its boot files.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - windows
  - recovery
kind: native
status: discovered
tools:
  - read
  - web.fetch
metadata:
  source: library
  library_id: windows-boot-repair
  official: true
  domain: ops
  security_flags: []
---

# Windows Boot Repair

## When to use
Windows will not start. The user runs commands in the recovery environment while you guide and read the output.

## Steps
1. Record the stop code or message and recent changes: update, disk clone, partition edit, firmware reset or new drive.
2. Ask whether the disk is encrypted and have the user locate the BitLocker recovery key before changing firmware or boot files.
3. Check firmware sees the drive. Clicking, disappearance or I/O errors means recover data first and stop repairing.
4. Try the built-in options first: Startup Repair, Safe Mode, uninstall the latest update, or a restore point.
5. In the recovery command prompt, use `diskpart` with `list disk` and `list vol` to identify the Windows volume; its letter is often not C:. If locked, unlock it with `manage-bde -unlock`.
6. Determine the layout: GPT with a FAT32 EFI system partition means UEFI.
7. For UEFI boot files, assign a free letter to the EFI partition and run `bcdboot <win>:\Windows /s <esp>: /f UEFI`.
8. For legacy BIOS, `bootrec /fixmbr`, `/fixboot` and `/rebuildbcd` apply; do not apply MBR fixes to a UEFI layout.
9. If system files are the cause, run offline checks with `sfc /scannow /offbootdir=<drive>:\ /offwindir=<win>:\Windows`.
10. Restart and confirm normal boot, then re-check encryption protection.

## Watch out for
- `format` or `clean` in diskpart on the wrong selection destroys data; formatting is not needed for these steps unless an expert has established the EFI partition itself is corrupt.
- Toggling storage mode or Secure Boot in firmware can itself stop boot or trigger recovery.
- Dual-boot machines share the EFI partition; preserve other loaders.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Windows boots normally twice with data intact, or the blocker is documented and data recovery is prioritised over reinstalling.
