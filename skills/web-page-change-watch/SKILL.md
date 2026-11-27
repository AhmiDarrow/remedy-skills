---
name: web-page-change-watch
version: 1.0.0
description: >
  Monitor a public page or feed for meaningful changes by comparing extracted values on a gentle schedule and notifying once. Use when someone wants to know when a price, notice, stock status or document changes.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - web
  - monitoring
kind: native
status: discovered
tools:
  - web.fetch
  - read
  - write
  - routines.create
  - routines.list
  - owner.notify
metadata:
  source: library
  library_id: web-page-change-watch
  official: true
  domain: data
  security_flags: []
---

# Web Page Change Watch

## When to use
The user wants to be told about a change instead of rechecking a page by hand.

## Steps
1. Ask exactly what change matters (a value, new list item, document version) and how soon they need to know. That sets the slowest acceptable interval.
2. Prefer a feed, API or official email alert if the site offers one. Check `robots.txt` and terms; do not monitor pages behind blocks or logins this way.
3. Fetch once and extract only the target, not the whole page, which changes with ads, timestamps and tokens.
4. Normalize whitespace, number and date formats and list order, using stable item ids for lists.
5. Save the baseline with URL, time and extraction rule, and show the user the extracted value to confirm it is the right thing.
6. Treat three results separately: unchanged, changed, and check failed (HTTP error, block page, selector matched nothing, implausible value). Never overwrite the baseline with a failed result.
7. Confirm a surprising change with one later refetch before notifying.
8. Check existing routines to avoid duplicates, then create one with the agreed interval.
9. Notify with old value, new value, time and link. Update the baseline only after the notification succeeds.
10. Alert once if checks keep failing, and agree when the watch should end.

## Watch out for
- A redesigned page can make "no change" true forever if a missing element reads as empty.
- Prices and availability may differ by region or session; tell the user what the check can see.
- Seeing an item available does not authorize buying or reserving it; stop and notify.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A test with an altered baseline produces exactly one notification, a broken selector reports failure, and the schedule appears in the routine list.
