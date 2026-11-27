---
name: browser-extension-vetting
version: 1.0.0
description: >
  Assess a browser extension's publisher, permissions, code behaviour and update risk before install or during a cleanup. Use when deciding whether an extension is safe or auditing those already installed.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
  - browser
kind: native
status: discovered
tools:
  - read
  - grep
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: browser-extension-vetting
  official: true
  domain: security
  security_flags: []
---

# Browser Extension Vetting

## When to use
A new extension is proposed, or an old collection of them has never been reviewed.

## Steps
1. List installed extensions with exact IDs, versions, enabled state and which browser profile. Names can be imitated; IDs identify.
2. Confirm the publisher's own site links to that exact store ID.
3. Read declared permissions and host access. Question access to all sites, cookies, request interception, history, clipboard, native messaging, debugger, proxy and management of other extensions.
4. Ask what the stated feature minimally needs. "Run when clicked" or specific sites is often enough.
5. Read the privacy policy for what is collected, shared or sold.
6. Search for reports of ownership transfer, injected ads, malware removal or sudden permission increases, and note the date of each source.
7. If source or the installed package is available, inspect the manifest, content script match patterns, outbound hosts and any remotely fetched configuration that steers behaviour.
8. Recommend remove, restrict site access, move to a separate browser profile, or keep, with reasons.
9. The user makes the changes. If an extension was malicious, advise signing out of active sessions from a clean profile and then changing passwords, and checking account activity.

## Watch out for
- Extensions update silently, so today's clean review does not cover a later owner.
- Disabling is not the same as removing, and sync can bring it back on other devices.
- A broad-access extension can read pages behind login, including banking and mail.
- A "verified" or "featured" badge is not a code audit.
- Do not read cookie stores or saved passwords as part of the review.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every extension in scope has a keep, restrict or remove decision tied to its permissions and evidence, with unverified points stated.
