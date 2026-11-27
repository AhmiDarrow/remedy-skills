---
name: empty-state-design
version: 1.0.1
description: >
  Design and build distinct states for first use, no results, load errors, no permission and cleared lists, each with a fitting next step. Use when screens show blank space or a misleading "no data".
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - ux
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
metadata:
  source: library
  library_id: empty-state-design
  official: true
  security_flags: []
---

# Empty State Design

## When to use
A list, table, dashboard or search view can have nothing to show.

## Steps
1. Find how the view gets data and which conditions currently collapse into the same blank output, such as `items?.length` treating loading and failure as empty.
2. Model the states explicitly: loading, first use, filtered or search empty, all done (inbox cleared), error, offline, no permission, not yet available (data still processing). Keep only those that can occur.
3. Check what the API returns so each can be told apart. If it returns 200 with an empty list on failure or denial, fix or report that.
4. For each write what happened, why if known, and one primary action: first use creates or imports; filtered empty shows the active query and clears filters; error retries and keeps entered input; no permission says who can grant it without revealing hidden items; all done may need no action.
5. Show create actions only to users allowed to create.
6. On refresh failure with existing data, keep the data visible and mark it stale instead of replacing it with an error.
7. Reuse the design system's component. Keep copy short and specific; decorative images get empty alt.
8. Keep toolbar and filters in place so users can recover, avoid layout jumps, and announce result changes such as zero results to screen readers.
9. Force each state through test data, a stub or a story and check at narrow width.

## Watch out for
- Flashing the first-use screen before the first response arrives.
- "You have no projects" after a failed request makes users think data was lost.
- Pagination left on page 3 after filtering looks like no results; reset the page.
- Raw error text exposing internals; log it and show a safe message with a reference if one exists.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every reachable state can be reproduced on demand, shows its own message and valid action, and a failed request never appears as empty data.
