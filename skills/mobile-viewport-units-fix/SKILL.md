---
name: mobile-viewport-units-fix
version: 1.0.0
description: >
  Fix full-height mobile web layouts broken by browser toolbars, the on-screen keyboard and display cutouts. Use when a bottom bar is hidden on phones or a 100vh screen scrolls oddly.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - mobile-web
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: mobile-viewport-units-fix
  official: true
  domain: frontend
  security_flags: []
---

# Mobile Viewport Units Fix

## When to use
A chat composer, bottom button or modal footer is cut off on a phone although it looks right in a desktop emulator.

## Steps
1. `grep` for `100vh`, `position: fixed` and `window.innerHeight` workarounds.
2. Pick the unit by intent. `dvh` tracks toolbars as they expand and collapse; `svh` fits even with toolbars showing, good for must-be-visible actions; `lvh` is the largest area, suitable for backgrounds. Keep a `vh` declaration first as fallback if old browsers are supported.
3. Where possible use a flex column with the footer in normal flow rather than fixed positioning plus compensating padding.
4. For notches and home indicators add `viewport-fit=cover` to the viewport meta, then pad with `env(safe-area-inset-bottom, 0px)` and the other sides.
5. Handle the keyboard separately: on some mobile browsers it overlays the layout viewport without resizing it. Listen to `window.visualViewport` resize and scroll to position a composer, or evaluate the `interactive-widget` viewport meta value where supported.
6. Contain scroll chaining in sheets with `overscroll-behavior: contain`.
7. Test on a real iOS and Android device: toolbars shown and hidden, both orientations, keyboard open, installed to home screen.

## Watch out for
- Desktop device emulation reproduces neither dynamic toolbars nor keyboard overlap.
- `dvh` on a large animated or text-heavy block can cause layout shifts while scrolling.
- Disabling zoom with `user-scalable=no` to stop focus zoom harms low-vision users; use an input font size of at least 16px instead.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
On both real platforms the primary action stays visible with toolbars and keyboard open, nothing sits under a cutout, and the page does not double scroll.
