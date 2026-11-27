---
name: data-export-user
version: 1.0.1
description: >
  Build a self-service export of a user's own data with complete scope, safe asynchronous delivery and no leakage of others' data. Use when adding "download my data" or portability to your product.
author: Remedy Official
license: Apache-2.0
tags:
  - privacy
  - backend
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
  library_id: data-export-user
  official: true
  security_flags: []
---

# Data Export User

## When to use
Users need a copy of the data your product holds about them.

## Steps
1. Derive scope from schemas, file storage and third-party stores, not from the settings screen. List each category as included or excluded with a reason, and have legal scope questions reviewed.
2. Define what happens to mixed data such as shared threads, comments from others or team files, so one person's export does not disclose another's private details.
3. Exclude password hashes, tokens, API secrets, internal risk notes and keys.
4. Choose formats a person and a program can use: JSON or CSV per category plus original uploaded files, with a manifest listing files, fields, timestamps with offsets and generation time.
5. Require re-authentication to request and to download. Rate limit, and allow one active job per user.
6. Run large exports as a background job that pages through data and streams to the archive. Make it resumable and record skipped items; never mark a partial archive as complete.
7. Store the archive privately, deliver it behind an authenticated check or short-lived link, and delete it after a stated period and on account deletion.
8. Notify without attaching the data, and tell the account owner an export was requested.
9. Test with a synthetic user holding every data type plus a second user, then open the archive and compare counts with the database.

## Watch out for
- CSV cells starting with `=`, `+`, `-`, `@`, tab or carriage return can run as formulas in spreadsheets; neutralize them.
- File names from user content can escape directories inside an archive.
- New tables silently missing later; add a test that fails when user-linked data has no export decision.
- An export is a prime target after account takeover.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The test archive's counts match the source for each included category, contains nothing of the second user's private data or any secret, and the link stops working after expiry.
