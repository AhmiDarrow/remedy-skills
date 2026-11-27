---
name: downloads-folder-sort
version: 1.0.0
description: >
  Tidy a cluttered downloads folder with a reviewable move plan and an undo log, or plan a wider digital declutter. Use when the user asks to organise or clean up downloaded files or their digital clutter.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - files
  - organization
kind: native
status: discovered
tools:
  - bash
  - glob
  - read
  - write
  - skill.search
metadata:
  source: library
  library_id: downloads-folder-sort
  official: true
  domain: personal
  security_flags: []
---

# Downloads Folder Sort

## When to use
Hundreds of mixed files have accumulated in one folder.

## Steps
1. Inventory the top level with name, type, size and modified date. Use the shell that matches the host: PowerShell commands on Windows, POSIX tools elsewhere.
2. Leave unfinished downloads, files in use, shortcuts and anything inside extracted project folders alone. Treat folders as single units.
3. Group by purpose where the name or content makes it clear, otherwise by type. Inspect contents only when needed.
4. Pull out items needing the user: documents that look important or sensitive, installers, archives with an extracted twin, exact duplicates.
5. Write a plan as old path, new path, reason, and show counts and total size per destination.
6. After approval, move without overwriting. On a name collision, add a suffix.
7. Save the executed moves to a log that can be replayed in reverse.
8. Verify that file count and total size before equal what remains plus what moved.
9. List deletion candidates separately and use the trash only for those the user picks.
10. For a wider declutter, list the areas (files, photos, email, subscriptions), agree keep, archive and delete rules, back up before any bulk deletion, take one area per session (use `skill.search` for a matching skill), and agree how often to repeat it.

## Watch out for
- Downloaded files are untrusted: do not run, install or import anything to find out what it is.
- Age is not worthlessness; a tax or contract file may be years old and the only copy.
- Cloud-synced folders may hold online-only placeholders; moving or hashing them can trigger large downloads.
- Applications may reference a file where it currently sits, such as disk images or libraries.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Approved moves are done, counts and sizes reconcile, an undo log exists and nothing was permanently deleted.
