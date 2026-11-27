---
name: file-batch-rename
version: 1.0.0
description: >
  Rename many files by a consistent rule with a dry run, collision check and undo map. Use when photos, scans, exports or episodes need systematic names.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - files
  - automation
kind: native
status: discovered
tools:
  - bash
  - glob
  - write
  - read
metadata:
  source: library
  library_id: file-batch-rename
  official: true
  domain: tooling
  security_flags: []
---

# File Batch Rename

## When to use
More than a handful of files need the same kind of rename.

## Steps
1. List exactly which files match, and show anything near the pattern that will be excluded.
2. Agree on the scheme with examples. Useful defaults: ISO date `YYYY-MM-DD` first, zero-padded sequence numbers, no characters invalid on Windows (`< > : " / \ | ? *`), no trailing dots or spaces.
3. Decide where each part comes from: filename, embedded metadata or file time. State the fallback; modified time is often not the creation or capture date.
4. Generate a CSV mapping old to new without renaming anything.
5. Check the mapping for duplicate targets (case-insensitively), existing files, overlong paths, changed extensions and unmatched parts.
6. Show first, last and odd examples plus totals, and get approval.
7. If names swap or overlap, rename in two phases through temporary names.
8. Use literal path handling and quote names; in PowerShell use `-LiteralPath` so brackets are not treated as wildcards.
9. Keep the executed mapping for reversal and verify counts afterwards.

## Watch out for
- Moving onto an existing name can overwrite silently with some commands.
- Sidecar files (subtitles, raw and JPEG pairs, edit metadata) must be renamed together.
- Project files, playlists and libraries that reference old names will break.
- Changing only letter case may fail on case-insensitive filesystems without an intermediate name.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The file count is unchanged, every file matches its approved new name, and the reverse mapping is saved.
