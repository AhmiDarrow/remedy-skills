---
name: image-provenance-check
version: 1.0.0
description: >
  Work out where a picture came from and whether its caption fits it. Use when a photo or screenshot is offered as evidence of an event, place or statement.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - research
  - sources
kind: native
status: discovered
tools:
  - read
  - bash
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: image-provenance-check
  official: true
  domain: docs
  security_flags: []
---

# Image Provenance Check

## When to use
Someone asks whether an image shows what the post says it shows.

## Steps
1. Get the largest, least re-compressed copy available and view it with `read`.
2. Check metadata with `exiftool file.jpg` if installed. Missing metadata is normal because most platforms strip it, and present metadata can be edited.
3. Describe what is visible before reading the caption: signs, language, plates, weather, shadows, landmarks, clothing, interface elements.
4. Search for the described content and distinctive visible text. If the user has a reverse image search service, ask them to run it or to approve using one, since that uploads the image to a third party.
5. Look for an earlier appearance. One predating the claimed event settles that the caption is wrong.
6. Test claims against details: does signage fit the country, foliage the season, the software layout the claimed date?
7. For screenshots of posts or articles, find the original on the account or site, or an archived copy. Fabricating a screenshot takes minutes.
8. Report in separate lists: established, consistent but unproven, and contradicted.

## Watch out for
- Visual oddities alone cannot prove an image is synthetic or edited, and a clean look cannot prove it is real. Do not give a confident verdict from appearance.
- Never identify a private person from a face.
- A genuine photo with a false place or date is far more common than elaborate fakery, so check context first.
- Do not upload private or sensitive images anywhere without explicit permission.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The earliest located source and each caption claim's status are stated, with unknowns left as unknown.
