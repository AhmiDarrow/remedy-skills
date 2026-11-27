---
name: seo-content-brief
version: 1.0.1
description: >
  Write a brief for one search-targeted page: intent read from real results, angle, outline, questions, evidence, internal links and success measures. Use before drafting an article meant to be found by search.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - seo
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: seo-content-brief
  official: true
  domain: content
  security_flags: []
---

# Seo Content Brief

## When to use
A writer needs direction for a single page that should answer a search need, without keyword stuffing.

## Steps
1. Get the topic, audience, what the business wants from the reader, and what the author knows first-hand that others do not.
2. Search the existing site (`grep` the content folder or `web.search` with a site filter) for pages already covering this need. If one exists, brief an update to it instead of a competing page.
3. Run `web.search` for the main query and close variants and read several top results with `web.fetch`. Record the dominant intent (learn, compare, buy, reach a specific site) and format (guide, list, tool, product page). Note that search results vary by place and time.
4. List what those pages all cover (expected), what they miss or get wrong, and which claims are unsupported. The angle comes from the gap plus the author's own evidence.
5. Collect reader questions from search suggestions, forums, support tickets or sales notes the user provides. Mark where each came from.
6. Outline with the direct answer early, one section per real question, and a note under each heading on what it must establish.
7. List required evidence: primary sources to cite, original data, screenshots, tests to run, expert checks (mandatory for health, legal or money topics).
8. Name internal links both ways, from real URLs: pages this one links to and pages that should link to it, with descriptive anchors.
9. Draft a title and meta description that match what the page delivers, and set measures with a review date: impressions and queries first, then clicks and the on-page action.

## Watch out for
- Inventing search volume or difficulty. Include numbers only from a tool export the user supplies.
- Copying the competitors' outline produces a page with no reason to rank or be read.
- Fixed word counts invite padding.
- No brief can promise a ranking; search engines may also rewrite titles and descriptions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The brief states intent with the observed results behind it, a distinct angle, an outline, sourced questions, required evidence, real internal links, title and meta drafts, and dated success measures.
