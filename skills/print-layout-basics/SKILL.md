---
name: print-layout-basics
version: 1.0.1
description: >
  Prepare a document for professional or home printing with correct page size, bleed, safe margins, resolution, colour handling, fonts and PDF preflight. Use before sending flyers, cards or booklets to print.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - print
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: print-layout-basics
  official: true
  domain: design
  security_flags: []
---

# Print Layout Basics

## When to use
Artwork or pages must print as intended and survive trimming and folding.

## Steps
1. Get the printer's specification first: finished size, bleed, safe margin, colour profile, PDF standard, total ink limit, binding, folds, paper and proofing. It overrides general defaults. For home printing, ask paper size and the printer's unprintable margin.
2. Set the document to the finished (trim) size. Add bleed outside it, commonly 3 mm or 0.125 in, and extend backgrounds to the bleed edge.
3. Keep text and logos inside the safe margin. Allow extra at the binding edge.
4. For folded or bound work, plan panel widths (an inner roll-fold panel is slightly narrower) and page counts (saddle stitching needs a multiple of four).
5. Check effective image resolution at placed size. About 300 ppi is the usual target for close reading; large work viewed from afar can use less if the printer agrees. Upsampling adds no detail.
6. Convert colour with the printer's profile near the end, and check brand and spot colours against their specified values. Remove accidental spot colours.
7. Set small black text to black ink only with overprint as the printer advises; use their rich black recipe for large areas. Avoid hairlines and tiny reversed type.
8. Embed or properly outline fonts, keeping an editable master.
9. Export the requested PDF. With Poppler available, run `pdfinfo -box file.pdf` for page boxes, `pdffonts file.pdf` for embedding and `pdfimages -list file.pdf` for image resolution.
10. Review every page at 100% and as a printed proof; the user approves and submits.

## Watch out for
- "Fit to page" scaling a bleed document.
- Crop marks that intrude into the bleed.
- Screen colours promising print colour; uncalibrated displays cannot.
- Transparency and overprint rendering differently between viewers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The file matches the printer's specification, preflight results are recorded with failures fixed or listed, and proof approval is obtained or shown as outstanding.
