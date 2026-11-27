---
name: reference-list-verification
version: 1.0.0
description: >
  Verify cited works exist, are not retracted and support their sentences. Use before submitting or publishing, or when references came from memory, secondhand notes or generated text.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - academic
  - citations
kind: native
status: discovered
tools:
  - read
  - web.search
  - web.fetch
  - write
metadata:
  source: library
  library_id: reference-list-verification
  official: true
  domain: docs
  security_flags: []
---

# Reference List Verification

## When to use
There is any chance that citations are wrong, misattributed or invented.

## Steps
1. List each citation with the exact sentence it supports.
2. Establish existence through a DOI resolver, publisher page, library catalogue or official repository. A search snippet or another paper's reference list is not enough.
3. Compare title, all authors, year, venue, volume and pages. A real DOI attached to a different title is a failure.
4. Access the work itself as far as legitimately possible and record the level: full text, partial, abstract only, record only.
5. Locate the supporting passage and note page, section or table.
6. Rate the fit: supports; supports a weaker version; background only; contradicts; cannot determine.
7. Detect secondary citation, where the source is itself citing someone else, and direct the author to the original or the style's "cited in" form.
8. For failures, suggest narrowing the claim, removing it or searching for real support. The author reads and approves replacements.
9. Check status: look for retraction, correction or expression-of-concern notices on the DOI landing page and in `https://api.crossref.org/works/` plus the DOI (coverage depends on publisher deposits), and in a retraction database. For preprints, read the version history, find any published version and compare the cited number.
10. Deliver a table of status with check date, evidence location and action.

## Watch out for
- Plausible authors, a real journal and a convincing title can still be a work that does not exist.
- Never repair a bad reference by substituting a similar paper without checking it against the claim.
- An abstract rarely settles a detailed methodological claim.
- A saved PDF will not show a later notice, and finding no notice does not certify the work.
- A retracted work cited on purpose must be labelled as retracted in text and reference entry.
- Chapters and conference papers are easily confused with journal versions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every reference is verified to exist with correct metadata, and each claim has a support rating or is visibly marked unchecked.
