---
name: keyword-intent-mapping
version: 1.0.0
description: >
  Group search queries by intent and assign each group to one page, finding gaps and cannibalisation. Use when planning which pages a site needs for search.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - seo
  - research
kind: native
status: discovered
tools:
  - read
  - write
  - web.search
  - web.fetch
  - bash
metadata:
  source: library
  library_id: keyword-intent-mapping
  official: true
  domain: content
  security_flags: []
---

# Keyword Intent Mapping

## When to use
There is a keyword list or search query export but no decision about which page answers what.

## Steps
1. Gather queries from the site's search console export, internal search, support questions and customer language. Treat third-party volume figures as estimates.
2. Normalise and deduplicate, keeping the metrics.
3. For important queries, look at the current results page. The page types ranking (guide, product, comparison, tool) show what searchers expect.
4. Cluster queries that the same results satisfy; split lookalike wording whose results differ.
5. Label intent: learn, compare, act, or find a specific site.
6. Map each cluster to one existing URL, a new page, or "not worth covering" with the reason.
7. Flag cannibalisation where several URLs get impressions for one cluster; propose merge, differentiate or redirect after checking each page's traffic and links.
8. Prioritise by business relevance and realistic ability to offer something better, then volume.

## Watch out for
- One page per phrasing variant, producing thin near-duplicates.
- Assuming results are the same in every country or device.
- Chasing high-volume terms with no link to what the business offers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every cluster has an intent label and exactly one destination or a stated exclusion.
