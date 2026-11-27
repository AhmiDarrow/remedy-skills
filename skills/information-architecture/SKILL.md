---
name: information-architecture
version: 1.0.1
description: >
  Structure a site or app's content and navigation from user tasks: inventory, grouping, labels, URLs and findability tests. Use when people cannot find things or menus have grown by accretion.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ux
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: information-architecture
  official: true
  domain: design
  security_flags: []
---

# Information Architecture

## When to use
Navigation, categories or documentation structure need designing or reorganising.

## Steps
1. Inventory content and features from routes, menus, sitemap or files (`glob`, `grep`). Record title, purpose, audience, owner, usage if known, and keep, merge or retire.
2. Collect the top tasks and the words people use from search logs, support tickets, interviews or analytics the user supplies. Label guesses.
3. Pick the primary organising principle (task, topic, audience, object, sequence). Use facets for attributes that cut across it instead of forcing one tree.
4. Group items and test grouping with a card sort when possible: open to learn people's categories, closed to check yours.
5. Draft the tree. Balance breadth against depth, keep sibling labels parallel and distinct, and avoid "Resources" or "Misc" as dumping grounds.
6. Label with user vocabulary, and record synonyms to feed search.
7. Plan routes besides menus: search, cross-links, landing pages, breadcrumbs, related items, and what differs by role or on small screens.
8. Tree-test the text hierarchy without visual design: write realistic tasks that do not reuse label words, and record success, first click and backtracking. Compare with the current tree where possible.
9. Revise, then give a map from old to new locations with URL redirects, in-app links, docs and bookmarks.

## Watch out for
- Mirroring the company's departments.
- Treating a card sort as the final design; it informs, it does not decide.
- Role-based entry points when people cannot tell which role they are.
- Reporting a tree test as done when only a paper review happened.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
There is an inventory with dispositions, a proposed tree with labels and rationale, alternative routes, a move and redirect map, and either test results or a ready-to-run test marked as not run.
