---
name: document-format-conversion
version: 1.0.0
description: >
  Convert documents between word-processor, Markdown, HTML and PDF formats and check what was lost. Use when a file must arrive in a format other than the one it was written in.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - conversion
  - files
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: document-format-conversion
  official: true
  domain: docs
  security_flags: []
---

# Document Format Conversion

## When to use
A format change is needed and fidelity matters.

## Steps
1. Ask what the recipient will do: edit, print, publish or archive. That decides what must be preserved.
2. Inventory risky features in the source: tables with merged cells, footnotes, equations, tracked changes, comments, fields, text boxes, custom fonts, images.
3. Pick the engine by goal. `pandoc in.docx -o out.md --extract-media=media` preserves structure, not page layout. `soffice --headless --convert-to pdf --outdir out in.docx` aims to preserve appearance.
4. When generating .docx with pandoc, pass `--reference-doc=ref.docx` to control styles.
5. For PDF to an editable format, warn that it is reconstruction; find the original source first.
6. Convert into a separate output folder, keeping the original.
7. Compare: count headings, tables, images and footnotes in both; render and view pages with complex features.
8. Check characters such as quotes, dashes, non-Latin text and symbols. In headless runs, missing fonts get substituted silently.
9. Report each loss and offer a manual fix or a different route.

## Watch out for
- A successful exit code says nothing about fidelity.
- Headless office conversion can fail or do nothing while the same program is open with another instance; check that the output actually exists and is new.
- Markdown cannot express merged cells or precise placement.
- Hidden comments and revisions may carry into the new format or vanish; decide deliberately.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The output opens, structural counts match or differences are explained, and the user knows what did not survive.
