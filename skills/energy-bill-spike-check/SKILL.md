---
name: energy-bill-spike-check
version: 1.0.0
description: >
  Find why a gas or electricity bill jumped by separating price, billing period, estimates and real usage. Use when an energy bill is unexpectedly high.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - home
  - bills
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: energy-bill-spike-check
  official: true
  domain: personal
  security_flags: []
---

# Energy Bill Spike Check

## When to use
A bill is much larger than expected and the cause is unknown.

## Steps
1. Collect the last 12 months of bills if possible, plus a photo of each meter today.
2. For every bill, extract: period start and end, days covered, units used, unit rate, standing charge, taxes, credits, and whether each reading was actual or estimated.
3. Compute units per day and cost per unit. This separates "more days" and "higher price" from "more use".
4. Check the meter number on the bill against the physical meter, and compare today's reading with the last billed one. A billed reading higher than today's means it is wrong, often an over-estimate, unless the meter was replaced or rolled over.
5. Compare with the same months last year, noting weather, new occupants, working from home, new appliances and tariff end dates.
6. If use really rose, measure: read the meter nightly and each morning to get overnight baseload, then use a plug-in energy meter, within its load rating, on plug-in suspects such as dehumidifiers, old freezers and portable heaters. For hard-wired loads such as immersion heaters and most pumps, compare meter readings across periods when they normally run and when they are normally off.
7. If the figures point to the supplier, draft a dispute with meter photos, the calculation and the correction requested. The person submits it; log the reference number.

## Watch out for
- Gas meters may read in volume while bills charge energy; use the conversion factor printed on the bill.
- A catch-up bill after several estimates looks like a spike but covers a longer shortfall.
- Leave consumer-unit and hard-wired testing to an electrician.
- Disputing a bill does not automatically pause payment; ask the supplier what happens to direct debits.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The increase is split into price, days, estimate correction and real consumption, with numbers for each.
