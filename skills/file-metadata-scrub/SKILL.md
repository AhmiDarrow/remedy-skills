---
name: file-metadata-scrub
version: 1.0.0
description: >
  Remove hidden personal data from photos, PDFs and office files before sharing, and verify the copies are actually clean. Use before publishing or sending files that may carry location, names or edit history.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
  - files
kind: native
status: discovered
tools:
  - bash
  - read
  - glob
  - write
metadata:
  source: library
  library_id: file-metadata-scrub
  official: true
  domain: security
  security_flags: []
---

# File Metadata Scrub

## When to use
Files are about to leave your control.

## Steps
1. Copy files to a separate output folder and keep originals untouched.
2. Inspect with `exiftool -a -G1 -s <file>` and note GPS, serial numbers, author, company, software, timestamps, comments and embedded thumbnails.
3. For images, strip with exiftool (`-all=`), keeping orientation and colour profile if appearance depends on them. Check whether it left `_original` backup files in the output folder.
4. For PDFs, know that exiftool's edits are reversible by design because old data remains in the file. After editing, rewrite the file (for example linearise with qpdf) or export a fresh sanitised copy.
5. Check PDFs also for annotations, attachments, form values, hidden layers, earlier revisions and text under black boxes. Use a true redaction tool that deletes content, then search and copy-paste to verify.
6. For office documents, use the application's document inspector, and check tracked changes, comments, speaker notes, hidden sheets and slides, external links, pivot caches and cropped images.
7. Check video and audio tags separately.
8. Look at the visible content too: faces, addresses, screens, badges, reflections and filenames.
9. For archives, inspect each member and remove stray folders such as `.git` and OS metadata files.
10. Re-run inspection on the final copies and open them to confirm they still work.

## Watch out for
- Cropping or covering may keep the hidden pixels or text.
- Some metadata, such as file structure details, cannot or need not be removed; report what remains.
- Cloud share links can expose uploader names and version history independent of file content.
- Do not batch-modify originals in place.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Final copies show no unwanted metadata or recoverable hidden content on re-inspection, open correctly, and originals are unchanged.
