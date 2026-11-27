---
name: error-message-catalog
version: 1.0.0
description: >
  Build a reference of a product's error messages with causes and fixes, taken from the source. Use when users or support keep searching for what an error means.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - errors
  - support
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - write
metadata:
  source: library
  library_id: error-message-catalog
  official: true
  domain: docs
  security_flags: []
---

# Error Message Catalog

## When to use
Errors are reaching users who have no page to look them up on.

## Steps
1. Search the code for error constructors, error codes and user-facing strings. Include the message catalog if strings are localised.
2. For each, trace the raising condition. The message often names a symptom; the condition shows the cause.
3. Collect frequency from support tickets or logs if available, and write the common ones first.
4. Use one entry shape: exact message (with variable parts marked), code, what happened, likely causes in order, how to confirm each, how to fix, what to send support if it persists.
5. Keep the searchable string verbatim in the heading or first line.
6. Group by what the user was doing, with an index by code.
7. Note messages that are misleading or give no next step and file them as product fixes.
8. Add a check or contributor note so new error codes get an entry.

## Watch out for
- Listing several causes with no way to tell them apart.
- Fixes that weaken security, such as disabling certificate verification or opening all permissions.
- Asking users to paste logs without telling them to remove tokens and personal data.
- Documenting unreachable internal assertions as user problems.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each included error links to its raising condition, has a confirm step and a fix, and its message text matches the source exactly.
