---
name: citation-style-check
version: 1.0.0
description: >
  Check in-text citations and the reference list against a required style and against each other. Use before submitting a paper, thesis or report with citations.
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
  - grep
  - bash
  - web.fetch
metadata:
  source: library
  library_id: citation-style-check
  official: true
  domain: docs
  security_flags: []
---

# Citation Style Check

## When to use
The writing is done and citation mechanics need to be right.

## Steps
1. Get the exact style and edition, plus local overrides from the course, journal or institution; those take priority. Consult the style's current official guidance when a rule is uncertain.
2. Extract all in-text citations and all reference entries, from footnotes too.
3. Match both directions: citations with no entry, entries never cited. Some styles' bibliographies allow uncited works, so check.
4. Compare author spellings, years and suffixes such as 2024a and 2024b.
5. Check that direct quotations have a page or other locator and that long quotes follow the block format.
6. Review entries by source type (article, chapter, web page, report, dataset) for required elements, order, capitalisation, italics, ordering of the list and DOI form.
7. Verify metadata against the DOI or publisher record; never fill a missing page range or year by guessing.
8. For numbered styles, confirm numbers follow the required order after edits.
9. Report corrections with location and rule, and apply mechanical ones if allowed.

## Watch out for
- Export from databases and reference managers often has all-capital titles, wrong item types or missing fields.
- Correct format does not mean the source supports the sentence; that is a separate check.
- Mixing conventions from two editions is easy to miss.
- Do not add sources the author has not consulted.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Citations and references match both ways, entries follow the named style, and unverifiable fields are flagged.
