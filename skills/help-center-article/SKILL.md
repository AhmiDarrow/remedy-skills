---
name: help-center-article
version: 1.0.0
description: >
  Write a task-based help article for end users that gets them to a result with minimal reading. Use when support answers the same how-do-I question repeatedly.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - support
  - help
kind: native
status: discovered
tools:
  - read
  - write
  - web.fetch
  - computer.navigate
  - computer.snapshot
  - computer.click
metadata:
  source: library
  library_id: help-center-article
  official: true
  domain: docs
  security_flags: []
---

# Help Center Article

## When to use
Non-technical users need to complete one specific task by themselves.

## Steps
1. Take the question's wording from real tickets or searches and use it as the title ("Change the email on your account").
2. Keep one task per article. Link out for related tasks.
3. Open with who can do it: required plan, role, platform. This saves readers from failing at step 5.
4. Walk the current interface with `computer.snapshot` and copy labels exactly. Stop before any step that saves, sends or buys on a real account.
5. Write numbered steps, one action each, location before action ("In Settings, select Members").
6. State what the user sees on success.
7. Add the two or three most common failures from tickets, each with a remedy.
8. Add alt text to screenshots and keep every instruction readable without them.

## Watch out for
- Directions by colour or position only ("the green button on the right"), which fail on mobile and for screen readers.
- Screenshots showing real names, addresses or account data; use test data such as Test User.
- Describing internal causes the reader cannot act on.
- Documenting from a spec instead of the shipped screen.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Following only the text on the current interface completes the task, and every quoted label matches the screen.
