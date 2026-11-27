---
name: conflicting-sources-resolve
version: 1.0.0
description: >
  Explain why two credible sources give different answers and decide what can honestly be said. Use when research turns up numbers, dates or findings that disagree.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - research
  - sources
kind: native
status: discovered
tools:
  - web.search
  - web.fetch
  - bash
metadata:
  source: library
  library_id: conflicting-sources-resolve
  official: true
  domain: docs
  security_flags: []
---

# Conflicting Sources Resolve

## When to use
Two sources you would normally trust cannot both be right as stated.

## Steps
1. Put the claims side by side with exact wording, date, and location in each source.
2. Test for a hidden difference before assuming error: definition, geography, population, time window, unit, currency, fiscal versus calendar year, rounding.
3. Check versions. One may cite a preliminary release, a superseded edition or text later corrected.
4. Check dependence: if one derives from the other or both from a third document, go to that document.
5. Compare methods: measured versus modelled, full count versus sample, what was excluded.
6. Where the underlying figures are available, recompute both and find the step where they diverge.
7. Decide by fit to the user's question and closeness to the evidence, and give the reason. If both are defensible, present the range and what drives it.
8. If nothing explains the gap, say it is unresolved and name what would resolve it.

## Watch out for
- Averaging two incompatible figures produces a number neither source supports.
- Majority voting fails when most pages copy one mistake.
- Newer is not automatically better; a recent summary can repeat an old error.
- Do not quietly drop the inconvenient source. The disagreement is often the useful finding.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cause of the difference is identified with evidence, or both claims are reported as unreconciled with their sources.
