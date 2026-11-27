---
name: lcp-diagnosis
version: 1.0.0
description: >
  Diagnose slow Largest Contentful Paint by splitting it into its four phases and fixing the one that dominates. Use when a page's main content appears late or LCP fails its target.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - performance
  - web-vitals
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: lcp-diagnosis
  official: true
  domain: frontend
  security_flags: []
---

# Lcp Diagnosis

## When to use
Field data or a lab audit shows slow LCP and the temptation is to apply a generic speed checklist.

## Steps
1. Get field data if it exists (analytics with web vitals, or public real-user reports) and note device class and percentile. The usual good threshold is 2.5 s at the 75th percentile. Lab runs explain; they do not prove what users see.
2. Record a trace with mobile throttling and cold cache on a production build. Identify the actual LCP element for that viewport.
3. Split the time into: time to first byte, resource load delay, resource load duration, and element render delay. Work on the largest part first.
4. TTFB: look at redirects, server rendering time, caching and CDN.
5. Load delay: the resource is discovered late. Put the image in the initial HTML as `img`, set `fetchpriority="high"`, remove lazy loading from it, or preload what CSS references.
6. Load duration: reduce bytes (dimensions, format, quality) and serve from a cached nearby origin.
7. Render delay: render-blocking CSS and scripts, client-only rendering, fonts hiding text, experiment snippets or fade-in animations that keep the element invisible.
8. Change one cause, then re-measure several runs and compare medians and the phase breakdown.

## Watch out for
- Shrinking an image does nothing when most of the time is load delay or render delay.
- The LCP element can differ between phone and desktop, or be a cookie banner.
- Preloading many things delays the one that matters.
- Field figures aggregate a trailing window, so a fix will not show immediately.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The LCP element and its phase breakdown are reported before and after, the targeted phase shrank across repeated runs, and any remaining gap is attributed to a named phase.
