---
name: image-prompt-brief
version: 1.0.0
description: >
  Write a structured prompt brief for an image generator and iterate on it one variable at a time. Use when the user wants generated artwork with a specific purpose and look.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - image
  - prompts
kind: native
status: discovered
tools:
  - write
  - read
  - clipboard.write
metadata:
  source: library
  library_id: image-prompt-brief
  official: true
  domain: content
  security_flags: []
---

# Image Prompt Brief

## When to use
A generated image must serve a real placement, not just look interesting.

## Steps
1. Pin down use, aspect ratio, minimum size, where text will overlay, and what the viewer must notice first.
2. Describe in order: subject and action, setting, composition and viewpoint, lighting, palette, medium or style, mood.
3. Use visible properties ("low side light, long shadows") over verdicts ("stunning, high quality").
4. State required empty space and anything to exclude, using whatever exclusion mechanism the chosen generator documents.
5. Write style as attributes instead of imitating a living artist or a protected character or brand.
6. Generate a small set, then change one element per round and log prompt, seed if exposed, settings and result.
7. Inspect at full size: hands, eyes, repeated objects, reflections, geometry, stray lettering.
8. Add exact text and logos afterwards in an editor.
9. Record the tool, its usage terms as of today, and that the image is generated, so the user can disclose it where required.

## Watch out for
- Realistic images of real people without consent, or fake documentary evidence.
- Assuming another tool understands the same weighting syntax.
- Rewriting the whole prompt each round, which teaches nothing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A chosen image meets ratio and size, passes the full-size defect check, and its prompt and terms note are saved.
