---
name: ffmpeg-size-target
version: 1.0.0
description: >
  Compress a video to fit a file size limit using calculated bitrate and two-pass encoding. Use when an upload or attachment rejects a file for being too large.
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
  library_id: ffmpeg-size-target
  official: true
  domain: content
  security_flags: []
---

# Ffmpeg Size Target

## When to use
There is a hard byte limit and quality should be as good as it allows.

## Steps
1. Confirm the limit and whether it means MB (1,000,000) or MiB (1,048,576). Aim about 5% under.
2. Get duration, resolution and frame rate with `ffprobe`.
3. Total kbit/s = target bytes * 8 / seconds / 1000. Subtract audio (for example 96 or 128 kbit/s) to get video bitrate.
4. Judge whether that bitrate suits the resolution. If very low, trim, scale down with `-vf scale=-2:720`, or lower the frame rate, and tell the user the trade.
5. Pass one: `ffmpeg -y -i in.mp4 -c:v libx264 -b:v 900k -pass 1 -an -f null /dev/null` (use `NUL` in Windows cmd or PowerShell).
6. Pass two: same video settings with `-pass 2 -c:a aac -b:a 96k -movflags +faststart out.mp4`.
7. Keep scale and frame-rate filters identical in both passes.
8. Check the byte size, then watch a high-motion section and small text.

## Watch out for
- Using CRF when the size must be guaranteed; CRF targets quality, not size.
- Picking a codec the destination cannot play.
- Mixing up kilobits and kilobytes, an eightfold error.
- Leftover pass log files confusing a later encode; run each job in its own folder.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The output is under the limit in bytes, plays in the target, and the user has seen any resolution reduction.
