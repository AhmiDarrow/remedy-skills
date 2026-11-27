---
name: lost-file-search
version: 1.0.0
description: >
  Track down a file the user saved but cannot find, from partial memory of name, content or date. Use when a document seems to have vanished.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - files
  - search
kind: native
status: discovered
tools:
  - bash
  - glob
  - grep
  - read
  - mail.list
metadata:
  source: library
  library_id: lost-file-search
  official: true
  domain: personal
  security_flags: []
---

# Lost File Search

## When to use
The file should exist and normal browsing has not turned it up.

## Steps
1. Gather clues: words in it, file type, application used, approximate last edit, how it arrived, and the last place it was seen.
2. Check the application's recent-files list and its default save and autosave locations.
3. Search likely roots by extension and date window before a whole-disk search.
4. Search by name fragments, then content with `grep`. Word, spreadsheet and slide files are zip containers, so plain text search misses their contents; use the OS index or extract text first.
5. Check trash, cloud-sync folders and their web trash and version history, external drives and the user's own other accounts or profiles. Do not search another person's profile just because admin rights allow it.
6. Look for the origin: a mail attachment or download that was opened from a temporary location and edited there.
7. Look for autosave and recovery files. Copy any candidate elsewhere before opening it, so it is not overwritten.
8. Show candidates with path, size and dates, and have the user confirm.
9. If a deleted file seems unrecoverable by these routes, stop writing to that drive and explain backup or specialist recovery options.

## Watch out for
- Opening and saving a recovery file can replace the only good version.
- Download or sync can change timestamps, so widen the date window.
- Temporary folders get cleaned automatically; act on candidates there promptly.
- Do not install recovery software onto the same drive without explaining the overwrite risk.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The user confirms the located file and it is copied to a safe place, or the searched locations and remaining options are listed.
