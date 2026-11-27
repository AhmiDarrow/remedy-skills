---
name: ffmpeg-clip-join
version: 1.0.0
description: >
  Join several video files with ffmpeg without glitches, picking the concat demuxer or concat filter. Use when merging recording segments or assembling clips into one file.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - ffmpeg
kind: native
status: discovered
tools:
  - bash
  - write
  - read
metadata:
  source: library
  library_id: ffmpeg-clip-join
  official: true
  domain: content
  security_flags: []
---

# Ffmpeg Clip Join

## When to use
Multiple files must play back to back as one.

## Steps
1. Probe each input and tabulate codec, resolution, frame rate, pixel format, time base, audio codec, sample rate, channels and stream order.
2. If all match, use the concat demuxer. Write `list.txt` with one `file 'clip1.mp4'` line per clip, in order.
3. Run `ffmpeg -f concat -safe 0 -i list.txt -c copy joined.mp4`. Use `-safe 0` only with a list you wrote yourself.
4. Quote names containing apostrophes correctly in the list, or rename working copies.
5. If properties differ, re-encode with the concat filter. Normalise each input first with `scale`, `pad`, `setsar=1`, `fps` and `aformat`, then `concat=n=3:v=1:a=1[v][a]` and map `[v]` and `[a]`.
6. Give a silent clip a matching silent track with the `anullsrc` source limited to its length, since every segment needs the same stream count.
7. Check output duration against the sum of inputs and watch each join.

## Watch out for
- Stream-copying mismatched files: ffmpeg may exit successfully yet the result freezes or desyncs.
- Shell glob order putting `clip10` before `clip2`.
- Stretching a different aspect ratio instead of padding or cropping.
- Variable frame rate phone footage drifting; convert to a constant rate.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Duration matches the sum within a fraction of a second and every join plays with sound in sync.
