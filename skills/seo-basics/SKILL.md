---
name: seo-basics
version: 1.0.1
description: >
  Check and fix on-page search basics on marketing or docs pages: titles, descriptions, headings, links, social previews and speed. Use before launching or revising public pages you control.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - marketing
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - glob
  - bash
  - web.fetch
metadata:
  source: library
  library_id: seo-basics
  official: true
  security_flags: []
---

# Seo Basics

## When to use
Public pages need sound on-page metadata and markup. If pages are missing from search results, diagnose crawling and indexing first.

## Steps
1. List page templates and sample each with real URLs or build output. Fix templates and shared metadata code rather than single pages.
2. Fetch the served HTML and record title, meta description, H1, canonical, robots meta, `lang` and social tags. Compare across pages to find duplicates, defaults and blanks.
3. Write each title to name that page's content, important words first. Descriptions summarise accurately; engines may rewrite either, and length limits are display guides, not rules.
4. Confirm indexing intent per page with the owner, so public pages are indexable, private and staging ones are not, and canonical and sitemap entries agree. Protect private content with authentication.
5. Check a clear main heading and logical outline, crawlable `a href` links with descriptive text, meaningful alt text and readable URLs. Redirect permanently when a URL changes.
6. For multiple languages, check each version has its own URL and reciprocal `hreflang` links including itself.
7. Add Open Graph tags with absolute image URLs for pages people share.
8. Check mobile rendering and Core Web Vitals. "Good" is LCP within 2.5 s, INP within 200 ms and CLS within 0.1 at the 75th percentile; one lab run is not field data.
9. Verify the built output and report fixes plus what needs content or owner decisions.

## Watch out for
- A shared layout default giving every page the same canonical or description.
- Keyword stuffing, hidden text or near-duplicate pages made for search engines.
- Promising rankings or traffic from these fixes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each sampled template serves unique accurate metadata with consistent indexing signals, in the built HTML, and speed results are labelled lab or field.
