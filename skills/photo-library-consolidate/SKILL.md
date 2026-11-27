---
name: photo-library-consolidate
version: 1.0.0
description: >
  Merge photos from phones, drives and cloud services into one backed-up library without losing originals or dates. Use when pictures are scattered or duplicated.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - tech-help
  - archive
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - glob
metadata:
  source: library
  library_id: photo-library-consolidate
  official: true
  domain: personal
  security_flags: []
---

# Photo Library Consolidate

## When to use
Years of photos need gathering and tidying safely.

## Steps
1. Inventory sources with counts and sizes. Check the destination has room for everything plus working copies.
2. Copy, never move, each source into its own staging folder. Cloud-only placeholders must be downloaded in original quality, using the service's export if offered.
3. Verify copies with counts and checksums before touching anything.
4. Find exact duplicates by file hash, for example `Get-FileHash` in PowerShell, `sha256sum` on Linux or `shasum -a 256` on macOS. Similar-looking shots are a separate, human review.
5. Keep paired files together: raw plus JPEG, motion photo clips, edit sidecars and exported metadata files, which may hold the only capture date.
6. Set folder dates from embedded capture time; do not trust file modified time. Send uncertain ones to an "undated" folder.
7. Dry run: produce a list of proposed moves and removals for approval. Quarantine duplicates rather than delete them.
8. Back up the finished library to a second device and an offsite copy, then restore a sample to prove it works.

## Watch out for
- Deleting in a synced folder removes photos on every linked device.
- Same filename from two cameras overwriting each other.
- Compressed messenger copies replacing full-size originals.
- Calling a sync service a backup.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Source counts reconcile with library plus quarantine plus listed exclusions, and a sample restore from backup opens.
