---
name: social-post-pack
version: 1.0.1
description: >
  Turn one announcement into a consistent set of posts adapted per channel, with link, alt text, schedule and replies prepared. Use when a launch, event or update needs posting in several places.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - social
kind: native
status: discovered
tools:
  - read
  - write
  - web.fetch
metadata:
  source: library
  library_id: social-post-pack
  official: true
  domain: content
  security_flags: []
---

# Social Post Pack

## When to use
One piece of news must be told in several places without contradicting itself or reading like copies.

## Steps
1. Write a fact sheet first: what happened, who it matters to, what they should do, link, date and time with zone, price or limits, approved quotes. Verify it against the source with `read` or `web.fetch`.
2. Confirm which accounts will post, and each channel's audience. Check current character limits and link preview behaviour instead of relying on memory.
3. For each channel write a version led by what that audience cares about: a short one-point post, a longer one with context, and a thread or carousel only if there are several distinct points.
4. Make the first line stand alone, since feeds truncate. Each thread item should make sense if shared by itself.
5. Give one call to action per post and test the link. Add tracking parameters only if the user measures them.
6. Use few, specific hashtags or none, following the account's existing habit. Write multiword tags in camel case so screen readers can read them.
7. Write alt text for every image describing what matters in it, including text shown in the image. Note captions for video.
8. Propose an order and times, respecting embargoes, with a follow-up post that adds something new.
9. Draft answers to the likely questions and complaints, and name who monitors replies.
10. Hand the pack to the user. They post or approve each one.

## Watch out for
- Identical text pasted everywhere, with handles that do not exist on that network.
- Invented quotes, user counts or urgency.
- A scheduled post that fires after the launch slipped. List what to cancel if it does.
- Sponsorships and affiliate links need visible disclosure.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every channel has a ready draft consistent with the fact sheet, with verified link, alt text, proposed time and reply notes, and nothing has been posted without the user.
