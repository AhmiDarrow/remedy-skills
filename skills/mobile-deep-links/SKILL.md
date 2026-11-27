---
name: mobile-deep-links
version: 1.0.0
description: >
  Set up and debug iOS universal links and Android App Links, including domain files and in-app routing. Use when links open the browser instead of the app or land on the wrong screen.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - mobile
  - navigation
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - web.fetch
metadata:
  source: library
  library_id: mobile-deep-links
  official: true
  domain: frontend
  security_flags: []
---

# Mobile Deep Links

## When to use
Adding verified web links to a mobile app, or fixing ones that work on one device and not another.

## Steps
1. Write a table of URL patterns, target screens, required parameters, auth requirement and web fallback.
2. iOS: add the Associated Domains entitlement `applinks:example.com` and serve `apple-app-site-association` at `/.well-known/` over HTTPS without redirects, listing team id plus bundle id and the matched paths.
3. Android: add intent filters with `android:autoVerify="true"` and serve `/.well-known/assetlinks.json` containing the package name and SHA-256 certificate fingerprints. Include the store's app signing certificate, not only the upload or debug key.
4. Fetch both files and check status, content type, redirects and every subdomain used. Apple devices usually fetch through a CDN, so changes may lag.
5. Check Android verification with `adb shell pm get-app-links <package>` and trigger a link with `adb shell am start -a android.intent.action.VIEW -d <url>`.
6. On iOS test by tapping a link in another app such as Notes; typing it into the address bar does not open the app.
7. Route through one parser covering cold start, already running and logged out, keeping the destination across login.
8. Treat every parameter as untrusted. A link must not perform a state-changing action without in-app confirmation.
9. Keep web pages working for people without the app.

## Watch out for
- Custom URL schemes can be claimed by other apps; never send secrets through them.
- On iOS, tapping a link to the same domain from within a browser page stays in the browser.
- Handling only the running-app callback drops cold-start links.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each table row opens the right screen on both platforms from cold, warm and logged-out states, verification reports success for each domain, and unknown paths fall back safely.
