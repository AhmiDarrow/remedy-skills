---
name: css-dead-style-removal
version: 1.0.0
description: >
  Find and safely delete unused CSS without breaking dynamic classes, states or third-party markup. Use when stylesheets have grown large and nobody knows which rules are still needed.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - cleanup
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - edit
  - bash
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: css-dead-style-removal
  official: true
  domain: frontend
  security_flags: []
---

# Css Dead Style Removal

## When to use
CSS keeps growing, old features have been removed from markup, and deleting rules feels risky.

## Steps
1. Measure built CSS size, raw and compressed, per route if split.
2. Collect two kinds of evidence. Static: search source, templates, CMS content and server strings for each selector's class. Runtime: the browser's Coverage panel across a written list of routes and states.
3. Treat coverage as evidence of use only. Unused in a session also covers hover, error, print, dark, mobile and permission-gated states you did not visit.
4. Search for constructed class names such as `` `btn-${kind}` `` or `'is-' + state`, and record the prefixes as kept.
5. Sort candidates: proven dead (feature and markup deleted), probably dead, and externally targeted (rich text, embeds, widgets).
6. Delete in small themed commits, starting with proven dead blocks and whole orphaned files.
7. Compare screenshots of the route and state list before and after each group.
8. For probably dead rules in high-risk areas, check version history for why they were added.
9. If adding automated purging to the build, configure its content globs and safelist from step 4, and diff the output.

## Watch out for
- An automatic purge that misses a template directory passes locally and strips styles in production.
- Removing a `@keyframes`, custom property or font face needs a search for the name in CSS and JavaScript, not just selectors.
- Reordering rules while tidying changes the cascade; keep deletion separate from reorganisation.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Built CSS is smaller by a reported amount, the route and state screenshots match, and each retained dynamic or external selector is recorded in the safelist or a comment.
