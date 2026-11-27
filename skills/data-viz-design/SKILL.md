---
name: data-viz-design
version: 1.0.1
description: >
  Design or correct a chart so it answers its question honestly and accessibly: chart type, aggregation, scales, labels, colour, uncertainty and text alternative. Use when making or reviewing a graph.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - data
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: data-viz-design
  official: true
  domain: design
  security_flags: []
---

# Data Viz Design

## When to use
A figure for a report, article or product must be clear, or an existing one may mislead.

## Steps
1. Write the question and the sentence the reader should be able to say afterwards. If one number or a small table answers it better, use that.
2. Inspect the data: grain, units, sample sizes, gaps, outliers, period completeness and any aggregation or smoothing already applied.
3. Match form to question: change over time to lines, category comparison to sorted bars, distribution to histogram, box or dot plot, relationship to scatter, parts of a whole to stacked or plain bars. Use pie only for very few clearly different shares.
4. Start bar and area values at zero, since length encodes the amount. Lines may use a narrower range if labelled; try a second range to check that the impression holds.
5. Prefer separate panels or indexed values to two y-axes. Label log scales plainly. Keep panels meant for comparison on shared scales.
6. Show real time spacing and break lines across missing data instead of joining or zero-filling.
7. Use colour for a purpose: one highlight against grey, an ordered ramp for magnitude, diverging only around a meaningful midpoint. Add labels, shapes or line styles so colour is not the only cue.
8. Title with the finding, subtitle with measure, unit and period, label series directly where possible, and cite the source. Show uncertainty and sample size when they affect the reading.
9. Annotate events and anomalies, without stating a cause the data does not show.
10. Add alternative text stating the takeaway, provide the data as a table, and view the chart at final size and in greyscale.

## Watch out for
- A cherry-picked start date that creates or hides a trend.
- Raw counts compared across groups of very different size.
- Bubble radius scaled to value exaggerates differences; scale area.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chart or its specification answers the stated question, scales and transformations are disclosed, it reads without colour, a text alternative exists, and data limitations are noted.
