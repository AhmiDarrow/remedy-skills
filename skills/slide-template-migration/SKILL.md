---
name: slide-template-migration
version: 1.0.0
description: >
  Move an existing presentation onto a new template while keeping content, notes and charts intact. Use when a deck must adopt a new house design or merge slides from several decks.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - slides
  - templates
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: slide-template-migration
  official: true
  domain: docs
  security_flags: []
---

# Slide Template Migration

## When to use
Slides need a different master and layouts.

## Steps
1. Back up both files. Export an image of every old slide and extract all text and notes as a baseline.
2. Inventory the template's layouts and placeholder types, and the old deck's special content: charts, tables, media, animations, linked files, hidden slides.
3. Make a mapping table from each old slide to a new layout.
4. Move content into real placeholders. Floating text boxes ignore the template and vanish from outline view and accessibility order.
5. Check theme colour remapping: charts and shapes tied to theme slots change colour, which can break a legend's meaning or make text invisible.
6. Keep charts editable with their data instead of flattening them where possible.
7. If scripting with a library such as python-pptx, test what it preserves on a few slides first; copying slides between files is not fully supported by every library. Use the application's reuse-slides feature when needed.
8. Render the result and compare side by side with the baseline, then diff extracted text and notes.
9. Remove unused old masters only after verification.

## Watch out for
- Slide aspect ratio changes stretch images and move objects.
- Hardcoded fonts and colours survive a template change and stand out.
- Footers, slide numbers and section names may need enabling again.
- Merged decks can carry confidential speaker notes from another audience.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Slide count and text match the baseline apart from listed edits, notes and media work, and slides use template layouts.
