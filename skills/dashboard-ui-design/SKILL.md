---
name: dashboard-ui-design
version: 1.0.1
description: >
  Design a dashboard around the decisions it supports: metric definitions, layout hierarchy, time and filter defaults, data states and drill-downs. Use when creating or untangling a metrics screen.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ui
  - data
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: dashboard-ui-design
  official: true
  domain: design
  security_flags: []
---

# Dashboard Ui Design

## When to use
A monitoring or reporting screen is being planned, or an existing one is a wall of tiles.

## Steps
1. Name the viewer, how often they look, and the three to five questions they must answer, with what they do for each answer. Cut tiles that change no action.
2. Classify the use: live operations, periodic review or exploration. Each needs different density, refresh and controls.
3. Define every metric: formula, unit, filters, source, freshness, owner. `grep` the code or queries to see how it is computed today, and flag two tiles that define one thing differently.
4. Give each headline number a reference: target, previous comparable period or normal range, and say which direction is good.
5. Lay out top to bottom as status, then explanation, then detail. Put related items together and the most important first in reading and focus order.
6. Set defaults for time range, time zone, comparison and filters. Show them on screen and keep them in the URL if views are shared. Say which tiles ignore a global filter.
7. Pick the simplest display per question: a number with trend, a line, sorted bars or a table.
8. Specify per tile: loading, no data yet, filtered to nothing, true zero, stale, partial, error and no permission. Show last-updated time.
9. Define drill-downs that carry the current filters through, and what narrow screens show first.
10. Enforce access on the server; hiding a tile is not protection.

## Watch out for
- An incomplete current day or week drawn like a finished one looks like a collapse.
- Red and green as the only status signal.
- A failed query rendered as 0.
- Auto-refresh that resets scroll, selection or focus.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A written spec maps each tile to a question and a defined metric, with layout order, defaults, every data state, drill-downs and access rules, and unresolved definitions are listed.
