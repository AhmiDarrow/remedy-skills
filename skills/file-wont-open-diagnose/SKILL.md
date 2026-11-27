---
name: file-wont-open-diagnose
version: 1.0.0
description: >
  Work out why a file will not open: wrong type, missing app, damage, blocking or encryption. Use when a user gets an error or gibberish opening a document, image or archive.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - files
  - troubleshooting
kind: native
status: discovered
tools:
  - bash
  - read
  - glob
metadata:
  source: library
  library_id: file-wont-open-diagnose
  official: true
  domain: tooling
  security_flags: []
---

# File Wont Open Diagnose

## When to use
Opening a specific file fails and the cause is unknown.

## Steps
1. Get the exact error text, the application used, where the file came from and whether it ever opened.
2. Copy the file and diagnose only the copy.
3. Check size. Zero bytes or far smaller than expected suggests an incomplete download or sync placeholder.
4. Identify the real type with `file` or by reading the first bytes: PDFs begin `%PDF`, zip-based office files begin `PK`, PNG shows `PNG` near the start. HTML in a "document" usually means a saved error or login page.
5. If the type and extension disagree, rename the copy and retry.
6. For zip-based files, test integrity with `unzip -t` or an equivalent.
7. Check permissions, a lock held by another program, path length, and whether it is marked as downloaded from the internet.
8. Try another viewer, and compare with a known good file of the same type to separate app faults from file faults.
9. If damaged, look for another source first: re-download, sender, version history, backup. Then try the application's repair feature on a copy.

## Watch out for
- An unexpected "document" that is really an executable or script, or asks to enable macros, should not be opened. Warn the user.
- Do not remove the operating system's blocking mark merely to make an unknown file run.
- Encrypted files need the password from its owner; do not attempt to crack it.
- Online repair sites receive the whole file.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cause is identified with evidence and the file opens from a safe copy or a replacement route is clear.
