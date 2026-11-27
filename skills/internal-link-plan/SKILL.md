---
name: internal-link-plan
version: 1.0.0
description: >
  Map a site's internal links to rescue orphan pages and strengthen important ones with descriptive anchors. Use when key pages get little traffic or are hard to reach.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - seo
  - structure
kind: native
status: discovered
tools:
  - glob
  - grep
  - read
  - bash
  - write
metadata:
  source: library
  library_id: internal-link-plan
  official: true
  domain: content
  security_flags: []
---

# Internal Link Plan

## When to use
A content site has grown without anyone deciding how its pages connect.

## Steps
1. Build the page inventory from the sitemap or content folder, with each URL's purpose and priority.
2. Extract links from content files or an authorised crawl of the user's site, separating body links from navigation and footer.
3. Compute inbound body links per page and click depth from the home page.
4. List orphans, important pages with few inbound links, links to redirects or 404s, and low-value pages that soak up links.
5. Group pages by topic; choose a hub for each group where one is useful.
6. For each proposed link give source page, the exact sentence it fits in, anchor text and target.
7. Use anchors that describe the destination; vary them naturally.
8. Apply approved edits, then rerun the extraction to confirm.

## Watch out for
- Automated linking of every occurrence of a phrase.
- The same anchor pointing to different pages, which confuses readers.
- Counting sitewide menu links as editorial support.
- Sentences bent out of shape to host a link.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
No priority page is orphaned, broken internal links are fixed or listed, and each added link has a natural host sentence.
