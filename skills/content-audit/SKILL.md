---
name: content-audit
version: 1.0.1
description: >
  Inventory a site or documentation set and decide per page to keep, update, merge, redirect or remove, with evidence. Use when content has piled up, contradicts itself or nobody knows what is current.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - web.fetch
  - bash
metadata:
  source: library
  library_id: content-audit
  official: true
  domain: content
  security_flags: []
---

# Content Audit

## When to use
A body of content needs a whole-collection review and a cleanup backlog.

## Steps
1. Define scope and the goals content should serve. Build the inventory from sitemap, repository or content system export plus analytics, since each misses pages.
2. Record per item: address, title, type, intended reader, task answered, owner and last substantive change.
3. Add evidence that exists: visits, search queries, conversions, inbound links and support references, over a window long enough to include seasonal use. Leave missing data blank.
4. Check accuracy against the current product or policy: versions, prices, steps, screenshots and links. An old date alone does not make a page wrong.
5. Cluster items answering the same question and note contradictions. For competing search pages, compare the queries each actually receives.
6. Assign keep, update, merge, remove or needs expert, with reason. Rare traffic does not justify removing legal, safety or reference pages.
7. For merges and removals choose the destination, list unique material to preserve and internal links to repoint. Redirect to a relevant replacement, not blanket to the home page.
8. Rank by user harm first (wrong or unsafe), then value against effort, with owners.
9. Get approval before unpublishing anything, and keep a copy.

## Watch out for
- Sampling a few pages and reporting it as a full audit; state coverage.
- Consent settings and tracking gaps making live pages look unused.
- Deleting pages that external documentation or the product links to.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every in-scope item has an evidence-backed decision, removals have redirect or retirement plans, and the prioritized backlog names owners.
