---
name: firmware-ota-rollback-design
version: 1.0.0
description: >
  Design over-the-air or field firmware updates that cannot brick a device, with verification and automatic rollback. Use when adding or reviewing an update mechanism for embedded hardware.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - embedded
  - firmware
  - reliability
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - write
  - bash
metadata:
  source: library
  library_id: firmware-ota-rollback-design
  official: true
  domain: security
  security_flags: []
---

# Firmware Ota Rollback Design

## When to use
Devices you own or build will receive new firmware after deployment.
## Steps
1. List constraints: flash layout, bootloader abilities, link reliability, power stability and whether anyone can physically recover a unit. Prefer the platform's established bootloader over writing one.
2. Choose a layout that always keeps one bootable image: dual slots, or a staging slot with a recovery image.
3. Define an image header with version, target hardware revision, length and hash, covered by a signature. The device holds only the public key; the private key stays off devices and out of the repository.
4. Verify the signature before marking an image bootable, and verify at boot according to the threat model.
5. Make state changes atomic: write the image, verify by reading back, then flip a power-fail-safe flag.
6. Boot new firmware on trial. It confirms itself only after real health checks such as reaching the update server; otherwise the watchdog or boot counter reverts.
7. Define anti-rollback for security fixes without blocking the automatic revert of a failed trial.
8. Plan data compatibility so the old image still reads settings after a revert.
9. Test on real hardware: cut power at many points, truncate and corrupt downloads, offer wrong hardware images and bad signatures, and ship a deliberately crashing build.
10. Roll out in stages, and ask the owner before pushing to any real fleet.
## Watch out for
- Programming secure boot fuses or locking debug ports is irreversible; require explicit confirmation and practice on spare units.
- A checksum alone detects corruption, not tampering.
- Confirming the image as soon as main starts defeats rollback.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every fault injection test ends with a device running a valid image and able to receive another update.
