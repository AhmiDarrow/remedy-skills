---
name: north-star-metric-tree
version: 1.0.0
description: >
  Choose a primary product metric and break it into input metrics teams can move, with guardrails. Use when teams track many numbers without knowing how they connect.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - product
  - metrics
kind: native
status: discovered
tools:
  - read
  - write
metadata:
  source: library
  library_id: north-star-metric-tree
  official: true
  domain: data
  security_flags: []
---

# North Star Metric Tree

## When to use
A product needs one agreed measure of delivered value and levers beneath it.

## Steps
1. State how customers get value and how often that naturally happens.
2. Propose two or three candidates counting value delivered, such as weekly accounts completing the core job.
3. Test each: can teams influence it, does it lead revenue or retention, can it rise while customers are worse off, can it be computed from existing data?
4. Define the chosen one exactly: unit, qualifying action, window, exclusions, data source.
5. Decompose into inputs such as breadth, depth, frequency and quality. Use arithmetic where true; label other links as hypotheses.
6. Give each input an owner and the work that could move it.
7. Add guardrails for quality, trust and cost.
8. Compute several past periods to see noise and seasonality before setting any target.

## Watch out for
- Revenue or raw signups as the only measure of value.
- Ratios that improve when the denominator shrinks.
- Drawing hypothesised links as if proven.
- Changing the definition without restating history.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The metric has a query-ready definition with past values, each input has an owner, and guardrails are listed.
