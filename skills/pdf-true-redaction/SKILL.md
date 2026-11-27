---
name: pdf-true-redaction
version: 1.0.0
description: >
  Permanently remove sensitive content from a PDF and prove it is gone. Use before sharing a document containing names, account numbers or other material that must not be recoverable.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - pdf
  - privacy
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: pdf-true-redaction
  official: true
  domain: security
  security_flags: []
---

# Pdf True Redaction

## When to use
Parts of a document must be unrecoverable by the recipient.

## Steps
1. Agree on the list of what to remove: exact strings, patterns, images, whole pages. Include variants such as initials, reference numbers and spaced digits.
2. Work on a copy and use a real redaction function (a PDF editor's apply-redactions step, or a library such as PyMuPDF where redaction annotations are then applied). A black rectangle alone leaves the text underneath.
3. If no reliable tool exists, black out rendered page images and rebuild the PDF from those flattened images, then OCR if search is needed.
4. Make sure image pixels under the boxes are removed too, not just text.
5. Strip document metadata, attachments, comments, form values, bookmarks, hidden layers and earlier incremental revisions. Rewrite the file fully rather than saving an update.
6. Verify: run `pdftotext` on the output and search for every listed string and variant; check `pdfinfo`, `pdfdetach -list` and `pdfimages`.
7. Render every page and inspect for missed instances, including headers, signatures, stamps and scans.
8. Have the user review the final copy before it leaves their machine.

## Watch out for
- Filenames, bookmarks and link targets often contain the very name being removed.
- Box width can hint at a short hidden word; use uniform blocks where that matters.
- Text search cannot find content inside images, so visual review is required.
- Whether redaction meets a legal disclosure duty is a question for a qualified person.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Text, metadata and attachment checks find none of the listed items, every page has been viewed, and the unredacted original is kept separate and clearly named.
