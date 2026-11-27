---
name: knitting-pattern-resize
version: 1.0.0
description: >
  Adjust a knitting or crochet pattern for a different gauge, yarn or size and recheck the stitch counts. Use when swatch gauge does not match or a size is missing.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - hobby
  - craft
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: knitting-pattern-resize
  official: true
  domain: personal
  security_flags: []
---

# Knitting Pattern Resize

## When to use
A maker wants a pattern to come out at specific measurements.

## Steps
1. Get the pattern's stitch and row gauge, finished measurements, stitch repeat, construction and the maker's measurements.
2. Ask for a swatch in the actual yarn, stitch and method (flat or in the round), washed and dried as the item will be, measured away from edges.
3. If changing needle or hook size can match gauge and the fabric is pleasing, prefer that to recalculating.
4. Compute counts as target measurement times new stitches per unit. Include intended ease.
5. Round to the pattern repeat plus edge stitches, and report the resulting width so the rounding is visible.
6. Handle rows separately. Recalculate shaping: number of changes over the available rows, distributed as whole rows.
7. Check joins agree: sleeve to armhole, picked-up edges, left and right fronts, matched stitch numbers where grafted.
8. Re-estimate yarn by fabric area from the swatch's weight, add a margin, and mark changes on a copy of the pattern.

## Watch out for
- Scaling every number by one ratio; neck depth, armholes and sleeve length follow the body, not gauge.
- Matching stitch gauge but ignoring row gauge in diagonal shaping.
- Substituting yarn by weight name only while fibre drapes differently.
- Redistributing a pattern for others without the designer's permission.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
New counts fit the repeat, shaping sums are consistent at every join, and resulting measurements are listed.
