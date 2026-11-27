---
name: subtitle-burn-and-embed
version: 1.0.0
description: >
  Add subtitles to video with ffmpeg, either burned into the picture or as a selectable track. Use when a finished video needs captions from an SRT or ASS file.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - subtitles
  - ffmpeg
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: subtitle-burn-and-embed
  official: true
  domain: content
  security_flags: []
---

# Subtitle Burn And Embed

## When to use
Caption files exist and must travel with the video.

## Steps
1. Decide which: a soft track can be switched off and keeps video untouched; burned-in always shows and requires re-encoding.
2. Confirm the subtitle file is UTF-8 and its timing matches this cut at the start, middle and end.
3. Soft in MP4: `ffmpeg -i v.mp4 -i subs.srt -map 0:v -map 0:a? -map 1 -c copy -c:s mov_text -metadata:s:s:0 language=eng out.mp4`. MKV can keep SRT or ASS directly.
4. Burn in: `-vf "subtitles=subs.srt" -c:a copy`. This needs a build with libass; check `ffmpeg -filters`.
5. Windows drive letters and backslashes break filter parsing. Run from the folder and use a relative file name.
6. Style SRT with `force_style`, for example `subtitles=subs.srt:force_style='FontSize=24,Outline=2'`, or edit an ASS file.
7. Make sure the font covers the language's characters, using `fontsdir` if needed.
8. Render a short sample at the longest caption first.

## Watch out for
- Assuming the destination platform shows embedded tracks; many want a separate caption upload.
- Auto-generated captions burned in unreviewed, especially names and numbers.
- Text over existing on-screen graphics.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
`ffprobe` shows the subtitle stream, or sampled frames show correctly rendered burned text, with timing checked in three places.
