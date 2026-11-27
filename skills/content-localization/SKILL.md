---
name: content-localization
version: 1.0.1
description: >
  Prepare articles, marketing pages, help content or documents for translators with a frozen source, context notes, glossary and review plan. Use before sending content to be translated.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - i18n
kind: native
status: discovered
tools:
  - read
  - write
  - glob
  - grep
metadata:
  source: library
  library_id: content-localization
  official: true
  domain: content
  security_flags: []
---

# Content Localization

## When to use
Written content is about to go into other languages. For translating app code strings, extract them into catalogs first.

## Steps
1. Confirm target locales (language and region), audience, formality, publish date and who translates and who reviews.
2. Inventory everything the reader sees: body, headings, buttons, alt text, captions, text inside images and video, page titles, meta descriptions, forms and follow-up emails.
3. Clean the source first: resolve drafts, replace idioms, puns and culture-bound references, use one term per concept, split tangled sentences. Where a line needs adaptation rather than translation, brief it with its intent.
4. Freeze a version and give it an id. Later edits go in a change list with old and new text.
5. Build a glossary: term, meaning, part of speech, approved translation if known. Add a do-not-translate list (owned product names, code, commands, interface labels that are not localised).
6. Add context per tricky item: where it appears, who is speaking, what a variable holds, screenshot, hard character limit.
7. Mark market-specific content for local decision: prices, currency, units, dates, legal text, support hours, links and images. Legal or regulated claims need a qualified local reviewer.
8. Export in a format that round-trips structure and ids, and test one file out and back before sending all.
9. Plan review: automated checks for missing segments and broken placeholders, in-layout check, and a native reviewer for high-visibility pages.

## Watch out for
- Sentences assembled from fragments cannot be reordered for another grammar.
- Silent source edits after handoff leave languages describing different products.
- Links that still point to source-language pages.
- Sending unpublished or personal data to an outside translation service without the owner's approval.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A frozen versioned source, glossary, do-not-translate list, context notes and named reviewer per locale are ready, and a test file survived the round trip.
