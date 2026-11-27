---
name: notes-app-migration
version: 1.0.0
description: >
  Move notes from one application to another and verify that text, attachments, dates and links arrived. Use when the user is switching note tools.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - notes
  - migration
kind: native
status: discovered
tools:
  - bash
  - read
  - glob
  - grep
  - write
metadata:
  source: library
  library_id: notes-app-migration
  official: true
  domain: personal
  security_flags: []
---

# Notes App Migration

## When to use
A collection must change tools without silent loss.

## Steps
1. Inventory the source: note and notebook counts, attachments, tags, internal links, tables, checklists, drawings, encrypted or shared notes, creation and edit dates.
2. Read what the source can export and what the destination can import; check current documentation for both versions.
3. Export in the richest format offered and keep that export as a read-only archive.
4. Pilot with about ten deliberately awkward notes and inspect them in the destination.
5. Decide handling for what will not transfer: convert, keep as PDF, or recreate by hand.
6. Fix conversion issues on a working copy with repeatable scripts: filenames, front matter, attachment paths, internal links.
7. Import fully, then compare counts of notes and attachments per notebook.
8. Spot-check old, long and attachment-heavy notes, plus searches the user runs often, including non-English text.
9. Keep the old account or files until the user has worked in the new tool for a while; deletion is their decision.

## Watch out for
- Locked or encrypted notes may be skipped without an error.
- Files stored only in the cloud may not be in a local export.
- Duplicate titles can overwrite each other when notes become files.
- File timestamps often reset on export, so preserve dates in metadata.
- Third-party converters see everything; ask before sending notes through an online service.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Counts reconcile with an explanation for each gap, pilot problem types are verified in the destination, and the original export is preserved.
