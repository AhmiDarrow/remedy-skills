---
name: logo-usage-rules
version: 1.0.1
description: >
  Document how to use a logo: approved versions, clear space, minimum sizes, backgrounds, co-branding, misuse and file choice. Use when partners or staff need rules for an existing mark.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - brand
kind: native
status: discovered
tools:
  - read
  - write
  - glob
metadata:
  source: library
  library_id: logo-usage-rules
  official: true
  domain: design
  security_flags: []
---

# Logo Usage Rules

## When to use
A logo exists and is being stretched, recoloured or placed badly. This documents use; it does not design a new mark.

## Steps
1. `glob` the asset folder and collect master vector files. List versions that really exist; ask which are approved. Report missing ones instead of inventing them.
2. Define the lockups (primary, horizontal, stacked, symbol only, wordmark) and when each is allowed.
3. Define clear space with a unit taken from the mark, such as the height of a letter, so it scales. Show it for each lockup.
4. Set minimum sizes separately for screen (px) and print (mm), based on rendering the finest detail. Provide a simplified small version only if approved.
5. List colour versions (full colour, one colour dark, reversed) with brand values for screen and print. Spot and CMYK values must come from the brand owner or a proofed specification.
6. State allowed backgrounds, including photos, with examples of where each version stays legible.
7. Cover special placements: avatar, favicon, app icon, embroidery or signage if relevant, and partner lockups with relative sizing, order and divider.
8. Show misuse: stretching, rotating, recolouring, effects, outlines, rearranging, retyping the wordmark, crowding, low contrast, upscaled screenshots.
9. Give a file table: SVG for web, vector PDF or the printer's requested format for print, transparent PNG where vector is unsupported, with a naming scheme.
10. Name who approves exceptions, and keep third-party use and trademark terms as items for the owner or a legal adviser.

## Watch out for
- Converting RGB to CMYK by calculator and presenting it as the brand colour.
- Live text in distributed SVGs, which changes when the font is absent.
- Minimum sizes never tested at actual size.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A saved guide covers each approved version with clear space, minimum sizes, colour and background rules, misuse examples and file selection, and missing assets or values are listed.
