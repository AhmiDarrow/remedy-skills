---
name: desktop-high-dpi-fix
version: 1.0.0
description: >
  Fix blurry or wrongly sized desktop app windows on scaled and mixed-DPI monitors without changing user display settings. Use when UI is fuzzy, clipped or shifts between screens.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - desktop
  - display
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: desktop-high-dpi-fix
  official: true
  domain: frontend
  security_flags: []
---

# Desktop High Dpi Fix

## When to use
A desktop app looks soft at 150% scaling, jumps size when dragged between monitors, or places popups in the wrong spot.

## Steps
1. Identify the toolkit, version and OS list. Record the scale factors where it fails.
2. Reproduce with an in-app, environment or toolkit scale override or offscreen rendering where available. Do not change the user's display scale or resolution; ask them to run real-monitor checks.
3. Whole window blurry on Windows usually means the process is not DPI aware and is being bitmap stretched. Declare per-monitor v2 awareness in the application manifest, or enable the toolkit's equivalent.
4. Handle scale changes at run time: on `WM_DPICHANGED` or the toolkit event, apply the suggested rectangle and rebuild fonts, cached bitmaps and layout.
5. Keep layout in logical units and convert to physical pixels once at the boundary. `grep` for hard-coded pixel sizes and mixed coordinate use in mouse, screen and window APIs.
6. Use vector icons or multiple raster sizes, including tray and window icons.
7. Size canvas and GPU surfaces at logical size times scale factor.
8. Snap hairlines and text origins to physical pixels at fractional scales.
9. Check popups, tooltips, drag images, saved window bounds and monitors with negative coordinates.

## Watch out for
- Integer-rounding the scale factor breaks 125% and 175%.
- Declaring awareness without handling it turns blurry UI into tiny UI.
- Mixing APIs that return virtualised and physical coordinates offsets clicks only on scaled monitors.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
At each listed factor, via override or user-run check, text is sharp, hit testing matches visuals and no content clips; anything unverified on real monitors is stated.
