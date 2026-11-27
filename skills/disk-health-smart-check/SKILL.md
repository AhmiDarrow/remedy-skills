---
name: disk-health-smart-check
version: 1.0.0
description: >
  Judge whether a drive is failing using SMART or NVMe health data and kernel errors, and protect data before replacing it. Use when there are I/O errors, odd slowness or a disk warning.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - storage
  - hardware
kind: native
status: discovered
tools:
  - bash
  - read
  - owner.notify
metadata:
  source: library
  library_id: disk-health-smart-check
  official: true
  domain: ops
  security_flags: []
---

# Disk Health Smart Check

## When to use
A drive is suspect or needs checking before being trusted.

## Steps
1. Identify the exact drive by model and serial, not just device letter.
2. Read OS evidence: kernel or System log for read errors, resets and timeouts.
3. If errors are active, copy irreplaceable data off first. Long tests and filesystem repairs add stress.
4. Run `smartctl -a <device>`; USB bridges and RAID controllers may need a `-d` device type.
5. On SATA, watch reallocated (attribute 5), current pending (197) and offline uncorrectable (198) sectors; nonzero and especially rising values are serious. Rising interface CRC errors (199) often implicate cable or connector.
6. On NVMe, read critical warning, media and data integrity errors, available spare against its threshold, percentage used and temperature.
7. Check the self-test log. If data is safe, run `smartctl -t long` and read the result after the stated time.
8. Compare with earlier readings; trend matters more than one vendor-specific raw number.
9. For a failing drive with unreadable data, image it onto a healthy disk with GNU ddrescue, keeping its map file, and recover from the image. If the data is critical, advise a recovery specialist before further attempts.
10. Record the verdict and replace by serial number.

## Watch out for
- An overall "PASSED" can appear on a drive that is already losing data.
- Raw values of some vendor attributes look alarming but are packed formats.
- Swapping source and destination in an imaging command destroys the original.
- In a degraded array, pulling the wrong disk can lose everything; match serials physically.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The drive is labelled healthy, monitor or replace with the readings that justify it, and at-risk data has a verified copy or its loss is reported.
