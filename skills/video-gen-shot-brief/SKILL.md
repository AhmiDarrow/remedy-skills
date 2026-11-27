---
name: video-gen-shot-brief
version: 1.0.0
description: >
  Break a short video idea into per-shot generator prompts with continuity anchors and a review log. Use when producing a sequence with a video generation tool.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - prompts
  - animation
kind: native
status: discovered
tools:
  - write
  - read
  - bash
metadata:
  source: library
  library_id: video-gen-shot-brief
  official: true
  domain: content
  security_flags: []
---

# Video Gen Shot Brief

## When to use
A generated video needs more than one lucky clip and the shots must belong together.

## Steps
1. Check the chosen tool's current limits: clip length, ratios, reference-image support, and cost per attempt. Agree a generation budget with the user.
2. Make a shot list with duration, purpose and the transition into the next shot.
3. Create a continuity sheet describing character, wardrobe, location, time of day, lens feel and palette in fixed wording.
4. Where supported, approve a still reference for each character and setting first.
5. Prompt each shot with one subject action and one camera move, plus start and end state.
6. Test the hardest shot first to find what the tool cannot do, and redesign around it with cutaways or stills.
7. Review each take for identity drift, morphing objects, physics and text; log keep or reject with the reason.
8. Assemble a rough cut with temporary sound before polishing. Handle titles, dialogue and music in editing.

## Watch out for
- Packing several actions into one short clip.
- Spending credits without the user's approval.
- Likenesses or voices of real people without permission.
- Presenting synthetic footage as a real event.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every shot has an accepted take or a stated substitute, the rough cut plays in order, and spend stayed within the agreed budget.
