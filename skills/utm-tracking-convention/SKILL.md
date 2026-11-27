---
name: utm-tracking-convention
version: 1.0.0
description: >
  Set a campaign link tagging convention and registry so analytics attribution stays clean. Use when campaign reports show messy, duplicated or missing sources.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - marketing
  - analytics
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: utm-tracking-convention
  official: true
  domain: data
  security_flags: []
---

# Utm Tracking Convention

## When to use
Several people tag links by hand and reports split one channel into many.

## Steps
1. Export current source, medium and campaign values and group the variants.
2. Check how the analytics tool in use maps medium values to channel groups, using its current documentation.
3. Define `utm_source` (where), `utm_medium` (channel type), `utm_campaign` (initiative), with optional `utm_content` for creative variants and `utm_term` for paid keywords.
4. Fix a short allowed list for source and medium, all lowercase, one separator. Values are case sensitive in many tools.
5. Choose a campaign naming pattern such as period plus initiative.
6. Make a registry sheet that builds the URL from dropdowns and logs owner and date.
7. Preserve existing query strings: add with `&` when `?` is present, and keep the `#` fragment after the query.
8. Click test links and confirm values survive redirects and appear in reports.

## Watch out for
- Tagging internal links on your own site, which can overwrite the original source.
- Putting emails, names or IDs in parameters.
- Redirects or link shorteners that drop the query string.
- Expecting old reports to be rewritten by a new convention.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A registry with allowed values exists and test clicks show the expected values in analytics.
