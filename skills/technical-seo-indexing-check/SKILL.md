---
name: technical-seo-indexing-check
version: 1.0.0
description: >
  Diagnose why pages are not being crawled or indexed by checking status codes, robots, canonicals and sitemaps. Use when pages are missing from search results.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - seo
  - debugging
kind: native
status: discovered
tools:
  - bash
  - web.fetch
  - read
  - grep
  - write
metadata:
  source: library
  library_id: technical-seo-indexing-check
  official: true
  domain: frontend
  security_flags: []
---

# Technical Seo Indexing Check

## When to use
Pages that should appear in search do not, on a site the user controls.

## Steps
1. Pick sample URLs: affected, healthy, and each page template.
2. Check status and redirects with `curl -sSIL URL` (on Windows use `curl.exe`). Expect one 200, no chains or loops. Some servers answer HEAD differently, so confirm with a GET.
3. Read `/robots.txt` for rules matching the paths.
4. Check for `noindex` in the robots meta tag and the `X-Robots-Tag` header.
5. Check `rel="canonical"`: absolute, returns 200, points where intended, and not every page pointing to the home page.
6. Compare raw HTML with the rendered page. Content or links appearing only after scripts run are at higher risk.
7. Check the sitemap lists canonical, indexable 200 URLs, and that affected pages have internal links.
8. Ask the owner for the search engine's URL inspection result, which shows its own view.
9. Report cause, evidence, fix and affected template.

## Watch out for
- Blocking a page in robots.txt to deindex it: crawlers then cannot see its `noindex`.
- A staging `noindex` or disallow shipped to production.
- "Soft 404" pages returning 200.
- Promising indexing after a fix; engines decide that.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each affected template has an identified blocker with captured evidence, or is confirmed technically indexable with remaining causes listed.
