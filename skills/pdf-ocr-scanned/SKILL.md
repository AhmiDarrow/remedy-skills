---
name: pdf-ocr-scanned
version: 1.0.0
description: >
  Make a scanned PDF searchable with OCR and measure whether the result can be trusted. Use for image-only scans, phone photos of documents or faxed pages.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - pdf
  - ocr
kind: native
status: discovered
tools:
  - bash
  - jobs
  - read
metadata:
  source: library
  library_id: pdf-ocr-scanned
  official: true
  domain: docs
  security_flags: []
---

# Pdf Ocr Scanned

## When to use
A PDF has no usable text layer and the user needs to search or extract it.

## Steps
1. Confirm with `pdffonts` and a test `pdftotext` run. Mixed files can have text on some pages only.
2. Check `ocrmypdf --version` and installed languages with `tesseract --list-langs`. Ask before installing anything.
3. Run on a copy: `ocrmypdf -l eng --rotate-pages --deskew in.pdf out.pdf`. Join languages with plus, as in `eng+deu`.
4. For mixed documents add `--skip-text` so pages that already have text are left alone. Use `--redo-ocr` to replace an earlier OCR layer; it cannot be combined with every image-processing option, so read the error if it refuses.
5. Reserve `--force-ocr` for broken text layers, because it rasterises every page.
6. If quality is poor, look at the source: under about 300 dpi, shadows, skew or bleed-through. A rescan beats more processing.
7. Verify three sample pages against images, concentrating on digits, names and table cells.
8. Search the output for a word you can see on a specific page to confirm the layer lines up.

## Watch out for
- Common confusions are 0 and O, 1 and l, rn and m, plus lost decimal points. Never use unverified OCR figures in calculations.
- Handwriting is generally unreliable with this tooling; say so instead of presenting guesses.
- Modifying a digitally signed PDF invalidates the signature. Keep the original.
- Tables come out as loose text, so searchable does not mean structured.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The new copy is searchable, the original is unchanged, and sample accuracy and weak pages are reported.
