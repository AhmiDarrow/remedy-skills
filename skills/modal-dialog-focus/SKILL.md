---
name: modal-dialog-focus
version: 1.0.0
description: >
  Make modals, drawers and confirmation dialogs accessible, with correct focus, dismissal, naming and background blocking. Use when building a dialog or when keyboard users get lost behind one.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - accessibility
  - components
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.key
  - computer.snapshot
metadata:
  source: library
  library_id: modal-dialog-focus
  official: true
  domain: frontend
  security_flags: []
---

# Modal Dialog Focus

## When to use
Tab escapes an open modal, closing it drops focus at the page top, or screen readers read the page behind.

## Steps
1. Find the dialog component in use and fix it once there. Prefer native `dialog` opened with `showModal()`, which provides the top layer, makes the rest inert and handles Escape.
2. With a custom implementation provide `role="dialog"`, `aria-modal="true"`, `inert` on background content and focus containment, or adopt a proven library.
3. Name it with `aria-labelledby` pointing at the visible title.
4. Choose initial focus on purpose: first field for forms, the least destructive button for confirmations, the heading or container for long text.
5. On close, return focus to the opener. If it no longer exists (the row was deleted), focus a logical neighbour.
6. Define dismissal: close button always; Escape; backdrop click only when nothing can be lost. With unsaved input, ask before discarding.
7. Lock background scrolling while keeping the dialog's own content scrollable, and keep actions reachable at small heights and 200% zoom.
8. For stacked layers, Escape closes only the top one, such as an open dropdown before the dialog.
9. Test with keyboard only and one screen reader.

## Watch out for
- Setting `aria-hidden` on an ancestor of the dialog hides the dialog too.
- The `open` attribute or `show()` produces a non-modal dialog with none of the modal behaviour.
- Toasts and portalled menus rendered outside a modal dialog are inert and unreachable.
- Autofocusing a destructive button lets a stray Enter confirm it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
By keyboard alone you can open, operate, dismiss and return to the exact prior place, focus never reaches the background, and the dialog is announced with its title.
