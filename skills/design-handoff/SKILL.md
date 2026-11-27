---
name: design-handoff
version: 1.0.1
description: >
  Prepare a design for engineering with final screens, states, component mapping, behaviour, content, assets, acceptance checks and open questions. Use when approved designs are about to be built.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - process
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: design-handoff
  official: true
  domain: design
  security_flags: []
---

# Design Handoff

## When to use
Developers must build from a design without guessing what the pictures leave out.

## Steps
1. List the final screens and flows with a version or date, and mark explorations as not to be built.
2. `glob` and `grep` the codebase for existing components and tokens. Map each design element to reuse, extend (say how) or new. Where design and code disagree, raise it.
3. Give spacing, type and colour as token names. Add measurements only where no token or layout rule covers it.
4. For each screen and component specify loading, empty, partial, error, success, disabled and permission states, plus hover, focus and pressed.
5. Describe behaviour the images cannot show: validation timing, defaults, sorting, limits, saving, undo, navigation, back button, interrupted and offline cases.
6. Stress the content: longest and missing values, huge counts, translation expansion, right-to-left if supported. State wrapping and truncation rules.
7. Describe layout changes between widths, plus keyboard order, focus movement, accessible names and announcements.
8. Specify motion with trigger, duration, easing and reduced-motion behaviour.
9. Export assets with consistent names, formats and sizes, noting fonts and images and their licences.
10. Write testable acceptance criteria, analytics events if required, open questions with owners, and who answers during the build. Walk it through with an engineer and plan a review of the built version.

## Watch out for
- Only the ideal-data screen is designed, so developers invent the rest.
- Detached or one-off values that look like tokens but differ slightly.
- Changing designs after handoff without a visible change note.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every in-scope screen has its states, behaviour and component mapping, assets are listed, acceptance criteria are testable, and open questions have owners.
