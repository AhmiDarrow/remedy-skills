---
name: search-traffic-decay-review
version: 1.0.0
description: >
  Find pages losing search traffic, work out why, and decide whether to refresh, merge, redirect or leave them. Use when organic traffic is slipping on an established site.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - seo
  - content-audit
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: search-traffic-decay-review
  official: true
  domain: data
  security_flags: []
---

# Search Traffic Decay Review

## When to use
Search performance exports show decline and the team's instinct is to rewrite everything.

## Steps
1. Export page and query data for two comparable periods, using year over year where demand is seasonal.
2. Rank pages by clicks lost, not by percentage, so tiny pages do not dominate.
3. For each, compare impressions, click-through and position. Impressions down with stable position suggests falling demand; position down suggests competition or relevance; click-through down alone suggests a changed results page or weaker title.
4. Rule out sitewide causes first: tracking changes, deploys, redirects, indexing errors, dates of announced engine updates.
5. Check query-level losses and look at the current results for them.
6. Review the page for outdated facts, missing subtopics searchers now expect, and overlap with your other pages.
7. Choose one action per page with evidence, then log the change date.
8. Recheck after a few weeks against untouched pages.

## Watch out for
- Changing only the publish date to look fresh.
- Deleting pages that still earn links or conversions.
- Averaged position hiding that the query mix changed.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each top losing page has a likely cause with data, one chosen action and a follow-up date.
