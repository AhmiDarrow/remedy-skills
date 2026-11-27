---
name: pagination-ui
version: 1.0.1
description: >
  Build numbered, previous-next or load-more list controls with URL state, stable results, focus handling and clear states. Use when adding or fixing pagination in an interface.
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
  - bash
metadata:
  source: library
  library_id: pagination-ui
  official: true
  security_flags: []
---

# Pagination Ui

## When to use
A list is too long to show at once, or paging loses place, filters or focus.

## Steps
1. Read the API contract first: page numbers or cursors, stable sort, whether a total exists, and the maximum page size. Do not invent page counts from a cursor API.
2. Choose the control: numbered pages when people jump, compare or cite positions; previous and next for cursors; load more for browsing. Avoid auto-only infinite scroll, which can make the footer unreachable.
3. Keep page or cursor, filters, sort and page size in the URL. Validate values and fall back safely on junk.
4. Reset to the first page when filter, sort or page size changes.
5. Use real links for page numbers and buttons for load more. Wrap page links in a labelled `nav`, mark the current one with `aria-current="page"`, and give icon-only arrows names.
6. After a page change, move to the list top and focus its heading. After load more, keep position, move focus predictably (such as to the first new item) and announce how many were added.
7. Keep old rows visible but marked busy while loading. Cancel or ignore stale responses so a fast double click cannot show the wrong page.
8. Handle empty list, failed next page with retry that keeps loaded rows, and a page beyond the end after deletions.
9. Test Back, refresh, shared link, narrow screen and keyboard only.

## Watch out for
- Offset paging over changing data duplicates or skips rows; sorting without a unique tiebreaker does too.
- Appending a page twice on retry; deduplicate by id.
- Back from a detail page after load more returning to only the first batch.
- A "select all" that silently means only the visible page.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
URL, Back and refresh restore the same view, rapid clicks never show mismatched rows, and keyboard and screen reader users can tell what changed.
