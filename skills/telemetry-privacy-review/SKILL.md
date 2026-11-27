---
name: telemetry-privacy-review
version: 1.0.0
description: >
  Review analytics and crash telemetry so only needed, non-identifying data leaves the device, with working consent and opt-out proven by traffic. Use before shipping or changing app telemetry.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
  - telemetry
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
  - edit
metadata:
  source: library
  library_id: telemetry-privacy-review
  official: true
  domain: security
  security_flags: []
---

# Telemetry Privacy Review

## When to use
An application sends usage events, crash reports or diagnostics.

## Steps
1. Write the questions the telemetry must answer. Data answering none gets removed.
2. Inventory every sender: your event calls, analytics and crash SDKs, update checks, embedded web content. Grep for SDK initialisation and endpoints.
3. For each event list all properties, including automatic ones: device ID, IP, locale, URL, screen names, breadcrumbs and previous log lines.
4. Look for accidental content: file paths containing usernames, query strings, form values, document titles, clipboard, exception messages, memory in crash dumps, session replay and screenshots.
5. Replace open strings with allow-listed values, counts or buckets. Avoid stable cross-product identifiers.
6. Check consent order: SDKs must not initialise or send before a required choice. Which choices require consent is a legal question to confirm.
7. Make opt-out stop collection and clear any queued events.
8. Verify retention, region, IP handling and vendor reuse settings.
9. In a test build with synthetic data, observe outbound traffic using an intercepting proxy on your own device, for first launch, normal use, error, opt-out and offline-then-online.
10. Add a schema check in tests that rejects unregistered events or properties, and publish a plain description.

## Watch out for
- SDK defaults often capture more than expected and change on upgrade.
- Events queued while opted out must not flush later.
- Removing a name field does not anonymise a rare combination of attributes.
- Server access logs record what the client payload omits.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Captured traffic matches the documented event list, opt-out and pre-consent states send nothing they should not, and a test blocks undeclared fields.
