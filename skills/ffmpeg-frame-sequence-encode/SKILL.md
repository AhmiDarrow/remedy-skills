---
name: ffmpeg-frame-sequence-encode
version: 1.0.0
description: >
  Encode rendered animation frames into video with correct frame rate, order, colour format and audio. Use when a numbered image sequence must become a deliverable file.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - animation
  - ffmpeg
  - video
kind: native
status: discovered
tools:
  - bash
  - glob
  - read
metadata:
  source: library
  library_id: ffmpeg-frame-sequence-encode
  official: true
  domain: content
  security_flags: []
---

# Ffmpeg Frame Sequence Encode

## When to use
An animation or render outputs numbered stills.

## Steps
1. List frames and check for gaps, zero-byte files and mismatched dimensions. A gap can silently end the sequence early.
2. Confirm the intended frame rate with whoever animated it.
3. Encode: `ffmpeg -framerate 24 -start_number 1 -i frame_%04d.png -c:v libx264 -crf 16 -pix_fmt yuv420p out.mp4`. In a Windows batch file double the percent sign.
4. Put `-framerate` before `-i`; it sets how input frames are timed.
5. For odd dimensions add a `pad` or `crop` filter to make both even.
6. Decide what happens to alpha. H.264 drops it, so composite over a background, or use a format that carries alpha such as ProRes 4444 via `prores_ks`.
7. Add audio with a second input, mapping both streams explicitly, and use `-shortest` only if truncation is intended.
8. Verify frame count with `ffprobe -count_frames -select_streams v:0 -show_entries stream=nb_read_frames -of csv=p=0 out.mp4`, and compare colours against a source still.

## Watch out for
- Linear EXR frames encoded without a colour transform, looking dark.
- Colour shifts from RGB to YUV conversion with untagged matrix.
- Deleting frames before the encode is verified.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Frame count and duration equal the source sequence at the chosen rate, and colour and alpha match the stated requirement.
