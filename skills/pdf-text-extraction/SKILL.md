---
name: pdf-text-extraction
version: 1.0.0
description: >
  Extract clean, correctly ordered text from a PDF and verify it. Use when copy-paste gives scrambled columns, odd symbols, missing spaces or nothing at all.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - pdf
  - extraction
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: pdf-text-extraction
  official: true
  domain: docs
  security_flags: []
---

# Pdf Text Extraction

## When to use
Text must come out of a PDF for quoting, searching or analysis.

## Steps
1. Diagnose before extracting: `pdfinfo in.pdf` for pages and encryption, `pdffonts in.pdf` for fonts. No fonts usually means the pages are images and need OCR.
2. In `pdffonts` output, a font with "uni" shown as no may extract as garbage.
3. Try `pdftotext in.pdf out.txt` first, which follows reading flow. Use `-layout` when position matters, as in forms or simple tables.
4. For a region such as one column, use the crop options `-x -y -W -H` with `-f` and `-l` to limit pages; confirm units in `pdftotext -h`.
5. Clean in a separate step: remove repeated headers, footers and page numbers; rejoin words hyphenated at line ends only when the joined form is a real word; expand ligature characters.
6. Keep page boundaries (form feed characters) if citations will be needed.
7. Compare several pages with their rendered images, including one with columns, one with a table and the last page.
8. If the mapping is broken, render pages with `pdftoppm -r 300 -png` and OCR them.

## Watch out for
- Blind de-hyphenation destroys real compounds such as "long-term".
- Invisible OCR layers can disagree with what is visible; the extracted text is not proof of what the page shows.
- Superscript footnote markers can fuse onto numbers and turn 12 plus note 3 into 123.
- If the file is password protected, ask the owner for the password through their own tool; do not try to crack it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Spot-checked pages match the visual document in content and order, and any pages that failed are listed.
