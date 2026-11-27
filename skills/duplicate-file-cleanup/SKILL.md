---
name: duplicate-file-cleanup
version: 1.0.0
description: >
  Find truly identical files by content, choose which copy to keep and remove extras reversibly. Use when storage is full of repeated photos, documents or backups.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - files
  - cleanup
kind: native
status: discovered
tools:
  - bash
  - jobs
  - glob
  - write
metadata:
  source: library
  library_id: duplicate-file-cleanup
  official: true
  domain: personal
  security_flags: []
---

# Duplicate File Cleanup

## When to use
The user suspects many copies and wants them reduced safely.

## Steps
1. Set the scan roots and exclude system, application, package and repository directories.
2. Group by size first, then hash only same-size files (`Get-FileHash` in PowerShell, `sha256sum` on Linux, `shasum -a 256` on macOS). A dedicated duplicate finder is fine if already installed.
3. Treat only matching content hashes as duplicates. Same name or size proves nothing.
4. Detect hard links, symlinks and junctions so one file reached by two paths is not counted twice.
5. For each group, propose a keeper by location rules the user agrees to, such as the organised library over downloads.
6. Report recoverable space and risky groups: inside project folders, application libraries or backup sets.
7. List near-duplicates (resized or re-encoded) separately for human review; never auto-remove them.
8. After approval, move extras to a quarantine folder or the trash, writing a manifest of original paths.
9. Confirm each keeper still exists and opens, and let the user decide later on permanent deletion.

## Watch out for
- A backup copy is a deliberate duplicate. Removing it removes the backup.
- Deleting in a synced folder deletes on other devices too.
- Moving to quarantine on the same drive frees no space yet; say so.
- Empty files all hash identically and are often meaningful markers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every removed file has a verified identical keeper listed in the manifest, and removal is still reversible.
