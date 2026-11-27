---
name: pdf-shrink-size
version: 1.0.0
description: >
  Reduce a PDF below a size limit while keeping it readable. Use when an upload or email rejects the file, or a short document is unexpectedly huge.
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
  library_id: pdf-shrink-size
  official: true
  domain: docs
  security_flags: []
---

# Pdf Shrink Size

## When to use
A PDF must fit a specific limit.

## Steps
1. Record the target size and what must stay legible (small print, stamps, photographs).
2. Find what takes the space: `pdfimages -list in.pdf` shows pixel dimensions, effective ppi, encoding and size per image. Check `pdffonts` for many embedded fonts.
3. Try lossless restructuring first: `qpdf --object-streams=generate --recompress-flate in.pdf out.pdf`.
4. If images dominate and have high ppi, downsample with Ghostscript (`gs`, or `gswin64c` on Windows): `gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -dNOPAUSE -dBATCH -sOutputFile=out.pdf in.pdf`.
5. If still too large, compare `/screen`, or set image resolution explicitly. For black-and-white scans, one-bit compression such as JBIG2 or CCITT is far smaller than colour JPEG; `ocrmypdf --optimize` can help if available.
6. Compare sizes each time; some files grow after rewriting, in which case keep the smaller original.
7. Zoom into the worst page (small text, signatures) and compare with the source.
8. Confirm page count, searchable text and links. If quality fails, offer splitting into parts if the recipient accepts that.

## Watch out for
- Lossy JBIG2 can substitute similar-looking characters, including digits. Use lossless mode for documents with numbers.
- Recompressing an already compressed output compounds damage; always start from the original.
- Ghostscript rewriting can drop tags, form behaviour or archival conformance.
- Signed files lose signature validity.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The output is under the limit, the hardest page is readable, and any lost feature is reported.
