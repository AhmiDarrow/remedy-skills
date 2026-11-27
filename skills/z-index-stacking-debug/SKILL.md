---
name: z-index-stacking-debug
version: 1.0.0
description: >
  Resolve overlays hidden behind other elements by finding stacking contexts rather than raising z-index. Use when a dropdown, tooltip or sticky header renders underneath something.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: z-index-stacking-debug
  official: true
  domain: frontend
  security_flags: []
---

# Z Index Stacking Debug

## When to use
An element with a huge `z-index` still sits below another, or fixing one overlay breaks a different one.

## Steps
1. Identify the hidden element and the one covering it, then list both ancestor chains up to their first common ancestor.
2. In each chain find what creates a stacking context: positioned element with `z-index` other than `auto`; `position: fixed` or `sticky`; `opacity` below 1; `transform`, `filter`, `perspective`, `clip-path`, `mask` or `mix-blend-mode`; `isolation: isolate`; `will-change` naming such a property; `contain: paint`; a flex or grid item with `z-index`; a container-type element in some engines, so check in the browser.
3. Compare the two contexts that are siblings under the common ancestor. Only their order matters; a child's number cannot escape it.
4. Also separate clipping from stacking: `overflow` other than `visible` clips regardless of `z-index`.
5. Prefer removing the accidental context. Otherwise render the overlay in the top layer (native `dialog.showModal()` or the `popover` attribute) or portal it to `body`.
6. Replace magic numbers with a short named scale of custom properties for base, sticky, dropdown, overlay and toast.
7. Add `isolation: isolate` to components whose internal numbers should not leak out.
8. Retest the original case plus open dialog with dropdown inside it.

## Watch out for
- A `transform` on an ancestor also makes `position: fixed` descendants position relative to that ancestor.
- Content portalled to `body` appears beneath a modal dialog in the top layer and is inert; render it inside the dialog.
- Portals move DOM position, so check inherited theme variables and outside-click logic.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The overlay displays above the intended content without clipping, the cause is named by element and property, and no new arbitrary large z-index was added.
