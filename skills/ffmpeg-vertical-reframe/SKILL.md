---
name: ffmpeg-vertical-reframe
version: 1.0.0
description: >
  Convert landscape video to vertical 9:16 by cropping, tracking sections or padding. Use when repurposing widescreen footage for phone-first short video.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - ffmpeg
  - social
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: ffmpeg-vertical-reframe
  official: true
  domain: content
  security_flags: []
---

# Ffmpeg Vertical Reframe

## When to use
Horizontal footage needs a portrait version without losing what matters.

## Steps
1. Probe size and rotation metadata; phone files can be stored sideways with a rotate flag.
2. Export frames at intervals with `-vf fps=1/5` and look where faces, hands, screen text and graphics sit.
3. Choose per section: fixed crop, shifted crop, stacked layout (speaker above screen), or full frame over a filled background.
4. Fixed centre crop to 1080x1920: `-vf "crop=ih*9/16:ih,scale=1080:1920,setsar=1"`. Add the x offset as a third crop value to move the window.
5. For a blurred background, `split` the input, scale one copy to cover and crop it with `boxblur`, scale the other to width 1080, and `overlay` it centred.
6. Make sure computed dimensions are even for yuv420p.
7. Encode segments with different offsets separately using identical settings, then join them.
8. Keep captions and key content clear of top, bottom and right edges where app controls sit; check the current platform's safe area guidance.
9. Review frames and playback on a phone-sized view.

## Watch out for
- Cutting off lower thirds or burned-in captions.
- Upscaling a narrow crop of 720p footage and promising it stays sharp.
- A crop that jumps mid-sentence.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Output is the target size, the subject stays in frame in sampled frames from every section, and text is unclipped.
