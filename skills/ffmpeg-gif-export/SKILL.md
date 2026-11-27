---
name: ffmpeg-gif-export
version: 1.0.0
description: >
  Make a small, clean GIF or looping clip from video with ffmpeg palette generation. Use when a short demo must autoplay in docs, chat or a pull request.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - image
  - ffmpeg
  - animation
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: ffmpeg-gif-export
  official: true
  domain: content
  security_flags: []
---

# Ffmpeg Gif Export

## When to use
A few seconds of motion need to be embedded where video may not play.

## Steps
1. Check whether the destination accepts silent MP4 or WebM; they are usually far smaller than GIF.
2. Trim to the essential seconds and crop to the region that changes.
3. Choose width and frame rate from the display size, for example 640 wide at 10 to 15 fps.
4. Use a generated palette in one command: `ffmpeg -ss 3 -t 5 -i in.mp4 -vf "fps=12,scale=640:-1:flags=lanczos,split[a][b];[a]palettegen=stats_mode=diff[p];[b][p]paletteuse=dither=bayer" -loop 0 out.gif`.
5. For gradients try other `dither` modes and compare; dithering trades banding for noise and size.
6. If over budget, cut duration first, then dimensions, then frame rate.
7. Check the loop point and hold the last frame briefly if the result needs reading time.
8. Provide alt text or a caption describing what happens.

## Watch out for
- Default conversion without a palette, which looks blotchy.
- Screen text unreadable after downscaling.
- Rapid flashing content; avoid more than three flashes per second.
- Long GIFs readers cannot pause.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The file meets the size budget, text is readable at display size, and the loop has been watched through.
