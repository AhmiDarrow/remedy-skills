---
name: metric-drop-investigation
version: 1.0.0
description: >
  Investigate a sudden metric change by ruling out data faults, then decomposing by segment, mix and funnel with a timeline. Use when someone asks why a number moved.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - analysis
  - debugging
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - write
metadata:
  source: library
  library_id: metric-drop-investigation
  official: true
  domain: data
  security_flags: []
---

# Metric Drop Investigation

## When to use
A business or product metric dropped or spiked unexpectedly and people want the cause.

## Steps
1. Pin down the change: exact definition, start time at the finest grain, size, and comparison basis.
2. Check it is unusual against the same weekdays, holidays and the series' normal variation.
3. Rule out data problems first: pipeline delay, partial day, duplicate or missing loads, event or schema change, new filter, time zone shift. Compare with an independent source such as database records or server logs.
4. Split a ratio into numerator and denominator, and see which moved.
5. Express the metric as a product or sum of components (traffic times conversion times order value) and locate the moving term.
6. Slice by platform, version, region, channel, customer type and payment or provider route. Rank slices by contribution to the total change, not by their own percentage swing.
7. Separate mix from rate: hold segment shares at the old values and recompute, then hold rates and vary shares.
8. Build a timeline of deploys, flags, config, pricing, campaigns, vendor incidents and tracking changes around the start (`git log` helps).
9. For each hypothesis, state what else must be true if it holds, and check that, including an unaffected group as control.
10. Report confirmed cause, likely cause or unknown, with the share of the change explained.

## Watch out for
- A coinciding event is not a cause; look for the effect only where the cause could reach.
- Slicing many ways will always find a dramatic small segment.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Data validity is established, the change is localized with contribution figures, and every claimed cause has a checked prediction.
