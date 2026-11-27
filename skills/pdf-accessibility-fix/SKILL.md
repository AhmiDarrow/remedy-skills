---
name: pdf-accessibility-fix
version: 1.0.0
description: >
  Make a PDF usable with screen readers and keyboard by repairing it at the source. Use when a document must be accessible or text is read out in the wrong order.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - pdf
  - accessibility
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
metadata:
  source: library
  library_id: pdf-accessibility-fix
  official: true
  domain: docs
  security_flags: []
---

# Pdf Accessibility Fix

## When to use
A PDF is being published to people who may use assistive technology.

## Steps
1. Check the basics: `pdfinfo` reports whether it is tagged and shows the title; a text extraction shows whether real text exists.
2. If the source document exists, fix it there: real heading styles in order, true list styles, table header rows, alt text on informative images, decorative images marked as such, descriptive link text, document language and title.
3. Export with the option that creates a tagged PDF. Printing to PDF usually discards tags.
4. Without a source, use a tagging-capable editor; OCR first for scans.
5. Run a validator that is available, such as veraPDF for PDF/UA or the editor's checker, and read each finding.
6. Test manually what validators cannot judge: reading order, whether alt text conveys the point, whether table cells announce their headers, tab order in forms.
7. Listen to at least a few complex pages with a screen reader, or ask the user to.
8. Offer an accessible HTML or word-processor version when the PDF cannot be repaired well.

## Watch out for
- "Tagged: yes" only means tags exist; they may all be plain paragraphs in the wrong order.
- Auto-generated alt text such as a filename passes checks and helps nobody.
- Colour alone must not carry meaning, and low contrast is a design fix in the source.
- Later merging or compressing can strip tags, so test the final file.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The final PDF has title, language, correct heading and reading order and meaningful alt text; remaining validator findings are listed and manual checks are described honestly.
