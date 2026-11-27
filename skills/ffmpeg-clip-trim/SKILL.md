---
name: ffmpeg-clip-trim
version: 1.0.0
description: >
  Cut a section out of a video with ffmpeg, choosing between fast stream copy and frame-accurate re-encode. Use when trimming clips or removing the start or end of a recording.
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
  - read
metadata:
  source: library
  library_id: ffmpeg-clip-trim
  official: true
  domain: content
  security_flags: []
---

# Ffmpeg Clip Trim

## When to use
A recording needs a segment extracted without an editing application.

## Steps
1. Inspect first: `ffprobe -hide_banner input.mp4` for codecs, duration, frame rate and streams.
2. Get start and end times and ask whether the cut must be frame exact.
3. Fast and lossless: `ffmpeg -ss 00:01:10 -i input.mp4 -t 25 -map 0 -c copy out.mp4`. Copying can only start cleanly at a keyframe, so the start may move or show frozen or black frames.
4. To see nearby keyframes: `ffprobe -select_streams v:0 -skip_frame nokey -show_entries frame=pts_time -of csv=p=0 input.mp4`.
5. Frame accurate: re-encode, for example `-ss 00:01:10 -i input.mp4 -t 25 -c:v libx264 -crf 18 -preset medium -c:a aac -b:a 192k`.
6. With `-ss` before `-i`, timestamps restart at zero, so use `-t` for length; do not assume `-to` still means the source time.
7. Write to a new file name; never overwrite the source, and do not add `-y` blindly.
8. Probe the output and play the first and last two seconds.

## Watch out for
- `-map 0` can fail when the output container cannot hold a data or subtitle stream; map the wanted streams explicitly.
- Checking only duration, which hides a bad first frame or audio offset.
- Re-encoding HDR or 10-bit footage with default settings without checking pixel format and colour tags.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The new file starts and ends where requested within the agreed tolerance, has the expected streams, and the source is untouched.
