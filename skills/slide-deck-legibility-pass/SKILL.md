---
name: slide-deck-legibility-pass
version: 1.0.0
description: >
  Fix slides that cannot be read from the back of a room or on a small screen share. Use when a deck is crowded, has tiny text, overflows or has weak contrast.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - slides
  - accessibility
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: slide-deck-legibility-pass
  official: true
  domain: design
  security_flags: []
---

# Slide Deck Legibility Pass

## When to use
The content is settled and the problem is that people cannot read it.

## Steps
1. Render all slides to images (convert to PDF with `soffice --headless --convert-to pdf`, then `pdftoppm -r 50 -png`). Reviewing thumbnails exposes what is unreadable.
2. List per slide: overflow, clipping, overlap, text below about 18 pt for projection, low contrast, unlabelled charts.
3. Cut or move words to notes before shrinking type. Split a slide with two ideas.
4. Turn paragraph bullets into short phrases, a table or a diagram only where the relationship supports it.
5. Check contrast, aiming at least for 4.5 to 1 for ordinary text, and do not place text over busy images without a solid backing.
6. Simplify charts: direct labels instead of distant legends, fewer gridlines, enlarged axis text.
7. Give every slide a unique title, set reading order, and add alt text to informative visuals.
8. Check that auto-fit has not quietly shrunk text, then re-render and compare.

## Watch out for
- Fonts absent on the presenting computer reflow every slide; embed them where allowed or use available ones, and test on that machine.
- Animations can stack objects that look overlapped in exports; inspect the build steps before deleting anything.
- Thin light grey text disappears on projectors even if it looks fine on a monitor.
- Do not change meaning while shortening; show the user any rewritten claim.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh render has no clipped or overlapping content, text meets the size and contrast floors, and every exception is listed.
