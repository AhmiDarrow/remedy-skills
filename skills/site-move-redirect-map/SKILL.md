---
name: site-move-redirect-map
version: 1.0.0
description: >
  Build and test a URL redirect map for a redesign, platform change or domain move. Use before URLs change on a live site so links and search traffic survive.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - seo
  - migration
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - web.fetch
metadata:
  source: library
  library_id: site-move-redirect-map
  official: true
  domain: ops
  security_flags: []
---

# Site Move Redirect Map

## When to use
Any change that alters existing public URLs.

## Steps
1. Collect old URLs from several sources: sitemap, authorised crawl, analytics landing pages, search export, server logs and known backlinks.
2. Normalise trailing slashes, case and parameters according to how the server treats them.
3. Map each old URL to its closest equivalent. If nothing equivalent exists, return 404 or 410 on purpose.
4. Use permanent redirects (301 or 308) for permanent moves.
5. Flatten chains so every old URL, including earlier redirects, goes straight to the final one.
6. Update internal links, canonicals, sitemap and structured data to new URLs.
7. Test the whole map on staging with a script that requests each old URL and compares status and `Location`; flag loops and non-200 targets.
8. Prepare rollback, then after launch rerun the test on production and watch 404 logs and traffic.

## Watch out for
- Redirecting everything to the home page, which strands users and is often treated as not found.
- Pattern rules that catch more paths than intended or drop query strings.
- Letting the old domain or certificate lapse.
- Shipping a staging robots block with the launch.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A scripted run shows every listed URL returning its intended status and target in one hop.
