---
name: url-as-ui-state
version: 1.0.0
description: >
  Move filters, tabs, sorting and selection into the URL with typed parsing, clean history and safe defaults. Use when views cannot be shared or bookmarked, or Back behaves unexpectedly.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - navigation
  - state
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: url-as-ui-state
  official: true
  domain: frontend
  security_flags: []
---

# Url As Ui State

## When to use
Refresh resets the view, a copied link shows something else, or each filter keystroke adds a history entry.

## Steps
1. List view settings and mark which a recipient of a link should see. Personal preferences and secrets stay out.
2. Choose placement: path segments for which resource, query parameters for how it is viewed, hash for in-page position.
3. Write one module that parses and serialises the parameters with types. Invalid or unknown values fall back to defaults without crashing; clamp page numbers and sizes.
4. Omit default values so canonical URLs stay short, and serialise in a stable order.
5. Make the URL the source of truth: components read from the router and write by navigating, with no mirrored local copy except an unsubmitted input draft.
6. Push a history entry for changes users think of as navigation (tab, opened record, page). Replace for continuous refinements such as typing or sliders, after debouncing.
7. Reset pagination when filters or sort change, in the same navigation.
8. Preserve unrelated parameters you do not own.
9. Version or alias renamed parameters so old bookmarks keep working.
10. Test copy into a new session, Back and Forward, and hand-edited nonsense values.

## Watch out for
- Two updates in one handler that each start from the old query string overwrite one another; merge into one.
- Tokens, emails or other personal data in URLs end up in logs, history and referrers.
- Two-way syncing between local state and URL with effects tends to loop or lag by one change.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A copied link reproduces the view in a fresh session, Back steps through meaningful changes only, and malformed parameters produce the default view without errors.
