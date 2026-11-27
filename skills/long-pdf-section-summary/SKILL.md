---
name: long-pdf-section-summary
version: 1.0.0
description: >
  Summarise a long PDF section by section with page references and a record of coverage. Use for reports, manuals or filings too long to read in one pass.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - summaries
  - pdf
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - todo
metadata:
  source: library
  library_id: long-pdf-section-summary
  official: true
  domain: docs
  security_flags: []
---

# Long Pdf Section Summary

## When to use
The document is long enough that skimming the start would pass for reading it.

## Steps
1. Run `pdfinfo file.pdf` for the page count, and check a sample with `pdftotext -f 1 -l 5 -layout file.pdf -` to confirm there is a text layer.
2. Read the table of contents and build a section map with page ranges. Note the offset between printed page numbers and PDF page indices.
3. Turn the map into `todo` items so no range gets skipped.
4. Ask what the reader needs it for; that decides which sections get depth.
5. Process one section at a time. For each, record main points, figures with units, decisions or requirements, and page numbers.
6. View pages with important charts or tables as images (render with `pdftoppm -r 100 -png -f <n> -l <n>`, then `read` the image), since text extraction loses their content.
7. Read appendices, footnotes and limitations wherever the main text refers to them.
8. Write the overall summary from the section notes, then verify each headline figure against its page.
9. State which pages were read closely, skimmed or skipped.

## Watch out for
- An executive summary is the authors' framing. Compare it with the body and report differences.
- Definitions near the front change the meaning of terms used much later.
- Two-column layouts can interleave lines in extracted text; render the page if sentences look scrambled.
- Never cite a page you did not open.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every section is accounted for, key figures carry verified PDF page numbers, and coverage gaps are listed.
