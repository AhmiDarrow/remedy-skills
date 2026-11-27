---
name: docx-style-cleanup
version: 1.0.0
description: >
  Replace hand-applied formatting in a Word-format document with consistent styles. Use when headings look random, numbering restarts or the table of contents is wrong.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - word-processing
  - formatting
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: docx-style-cleanup
  official: true
  domain: docs
  security_flags: []
---

# Docx Style Cleanup

## When to use
A document edited by several people has direct formatting piled on top of itself.

## Steps
1. Copy the file and render the original to PDF as a visual baseline (`soffice --headless --convert-to pdf --outdir baseline in.docx`).
2. Inventory paragraphs with an installed library such as python-docx: style name, text start, and direct overrides. A .docx is a zip, so `word/document.xml` and `word/styles.xml` can be inspected when the library hides something.
3. Infer the intended hierarchy and show the mapping: bold 14 pt line becomes Heading 1, manual dash becomes a list style.
4. Define font, spacing and keep-with-next once in the styles.
5. Apply styles, then clear redundant direct formatting while keeping meaningful italics, bold terms, superscripts and links.
6. Replace typed numbers and bullets with real list numbering, and runs of empty paragraphs or tabs with spacing, page breaks or tables.
7. Update the table of contents and cross-reference fields in a word processor, since libraries generally do not calculate fields.
8. Render again and compare page by page with the baseline; check text content is unchanged by diffing plain-text exports.

## Watch out for
- Stripping all run formatting erases italic titles, chemical subscripts and emphasis.
- A paragraph's text can be split across many runs, so naive string replacement misses matches or flattens formatting.
- Section breaks hold margins, orientation and headers; deleting one changes distant pages.
- Fonts missing on this machine shift layout in the render without any file change.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Headings and lists use styles, the navigation outline matches the intended structure, and the text diff shows only intended differences.
