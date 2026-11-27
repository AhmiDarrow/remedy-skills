---
name: image-batch-export
version: 1.0.0
description: >
  Batch resize and convert images for the web or a client while keeping originals, colour and privacy intact. Use when a folder of photos or graphics needs consistent exports.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - image
  - workflow
kind: native
status: discovered
tools:
  - bash
  - glob
  - read
  - write
metadata:
  source: library
  library_id: image-batch-export
  official: true
  domain: content
  security_flags: []
---

# Image Batch Export

## When to use
Many images need the same sizes, formats or naming.

## Steps
1. Inventory dimensions, formats, colour profiles, transparency and orientation tags. ImageMagick `identify` does this if installed; check the version.
2. Agree each output: longest edge or exact box, crop or fit, format, size budget, naming.
3. Write only into a new output folder.
4. With ImageMagick 7, a fit-within resize that never enlarges is `magick in.jpg -auto-orient -resize "1600x1600>" -quality 82 out.jpg`. Quote the `>` so the shell does not redirect.
5. Convert to sRGB for web with the proper profiles before removing metadata; stripping a wide-gamut profile first shifts colour.
6. Remove location and device metadata from public files, then verify with a metadata reader. Keep copyright fields if the owner wants them.
7. Use JPEG, WebP or AVIF for photos according to what the destination accepts; keep PNG or lossless for sharp graphics and alpha.
8. Test on five representative files, review at full size, then run the batch and compare counts.

## Watch out for
- `mogrify` overwriting originals when no output path is set.
- Transparency turning black when saved as JPEG; flatten onto a chosen background.
- Name collisions such as `a.png` and `a.jpg` both becoming `a.webp`.
- Animated or multi-page inputs producing several files.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Output count matches the plan, sampled files meet dimensions and budgets, GPS data is absent from public outputs, and originals are unchanged.
