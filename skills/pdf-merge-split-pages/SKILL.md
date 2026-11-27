---
name: pdf-merge-split-pages
version: 1.0.0
description: >
  Combine, split, reorder, rotate or delete PDF pages without losing content. Use when assembling a submission packet or pulling pages out of a larger file.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - pdf
  - files
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: pdf-merge-split-pages
  official: true
  domain: docs
  security_flags: []
---

# Pdf Merge Split Pages

## When to use
The task is page-level assembly, not editing text.

## Steps
1. List the inputs in the intended order and get each page count with `pdfinfo`.
2. Write the page plan (file, range, rotation) and confirm it if order matters for a submission. Printed page numbers may differ from PDF indices.
3. Merge: `qpdf --empty --pages a.pdf b.pdf 2-4 -- packet.pdf`.
4. Extract: `qpdf in.pdf --pages . 1-3,7 -- part.pdf`. Burst into single pages with `qpdf --split-pages in.pdf page-%d.pdf`.
5. Rotate: `qpdf in.pdf out.pdf --rotate=+90:2-3`.
6. Always write to a new filename; keep originals.
7. Verify the output page count equals the planned sum, then render the first, last and boundary pages with `pdftoppm -r 60 -png` and look at them.
8. Check what must survive: bookmarks, links, form fields and attachments. Page assembly does not always carry document-level features as expected.

## Watch out for
- Shell globs sort a hand-named `page-10` before `page-2`; list inputs explicitly or zero-pad their numbers.
- Merging forms with identically named fields can make them share one value.
- Any change breaks digital signatures. Tell the user before assembling signed documents.
- Do not upload the files to an online merge site without permission; they may contain private data.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The new file has the planned page count and order, verified visually at the joins, with originals intact and lost features noted.
