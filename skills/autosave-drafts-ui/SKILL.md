---
name: autosave-drafts-ui
version: 1.0.0
description: >
  Implement autosave for editors and forms with debouncing, honest save status, local recovery and conflict handling. Use when users lose work or saves overwrite each other.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - forms
  - resilience
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: autosave-drafts-ui
  official: true
  domain: frontend
  security_flags: []
---

# Autosave Drafts Ui

## When to use
A document, settings editor or long form should save without a button, or the current autosave silently loses edits.

## Steps
1. Decide what autosaves. Drafts suit it; settings with immediate side effects or published content need an explicit action.
2. Model status as dirty, saving, saved and failed, with a revision counter incremented on each edit.
3. Debounce after typing pauses (around a second) and add a maximum wait so continuous typing still saves.
4. Allow one request in flight. When it returns, if the revision moved on, send the latest. Mark saved only when the acknowledged revision equals the current one.
5. Send a server version or ETag with each write. On a conflict, keep both copies and let the user choose or merge; never overwrite silently.
6. Retry transient failures with backoff and a visible message. Stop retrying on validation or permission errors and say what to fix.
7. Keep a local recovery copy keyed by user and document, remove it after confirmed save, and offer restore when it is newer.
8. Flush on blur, route change and `visibilitychange` to hidden. Warn with `beforeunload` only while unsaved changes exist.
9. Test offline, slow network, two tabs and expired session.

## Watch out for
- Replacing editor content with the save response moves the cursor and discards characters typed during the request.
- `unload` handlers are unreliable, especially on mobile; do not depend on them for the final save.
- Showing Saved when the request was merely queued destroys trust.
- Shared computers make unencrypted local drafts a privacy problem; clear them on logout.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Under throttled and offline conditions no typed text is lost, status text matches server reality, and a two-tab edit produces a visible conflict instead of an overwrite.
