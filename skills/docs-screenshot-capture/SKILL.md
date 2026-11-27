---
name: docs-screenshot-capture
version: 1.0.0
description: >
  Capture consistent, safe screenshots for documentation using test data and repeatable settings. Use when guides need new or refreshed interface images.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - screenshots
  - media
kind: native
status: discovered
tools:
  - computer.snapshot
  - computer.screenshot
  - computer.windows
  - computer.window
  - computer.click
  - computer.type
  - bash
  - write
metadata:
  source: library
  library_id: docs-screenshot-capture
  official: true
  domain: docs
  security_flags: []
---

# Docs Screenshot Capture

## When to use
Interface images in docs are missing, outdated or inconsistent.

## Steps
1. List the shots needed, each tied to a step. Skip images that show only a single obvious button.
2. Fix capture conditions in a note: window size, theme, language, zoom. Do not change the system's display scale or resolution to get them; resize the window.
3. Prepare a test account with invented data such as Test User and addresses at example.com.
4. Close notifications, other tabs and anything personal; check title bars, address bars, sidebars and avatars.
5. Bring the interface to state without pressing buttons that send, buy or delete.
6. Capture and crop to the region plus enough context to locate it.
7. Redact by painting solid blocks over pixels in the saved image. Blur and pixelation can sometimes be reversed.
8. Name files by feature and state, add alt text, and keep annotation style uniform in an editable source.

## Watch out for
- Tokens in URLs and keys visible in settings screens.
- Covering a secret with a movable layer that survives in the published file.
- Lossy compression that makes small UI text unreadable.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every listed shot exists, was inspected at full size for personal data, has alt text, and shows the current interface.
