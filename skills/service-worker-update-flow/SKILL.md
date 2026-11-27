---
name: service-worker-update-flow
version: 1.0.0
description: >
  Fix web apps stuck on old versions by designing service worker caching, update prompts and safe activation. Use when users must hard-refresh or see broken assets after a deploy.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - pwa
  - caching
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - computer.navigate
metadata:
  source: library
  library_id: service-worker-update-flow
  official: true
  domain: frontend
  security_flags: []
---

# Service Worker Update Flow

## When to use
Deploys do not reach users, chunk loads fail afterwards, or offline support is being added to an existing app.

## Steps
1. Read the current worker and its registration, and identify whether a build plugin generates it. Inspect the Application panel: registered, waiting, active, and cache contents.
2. Assign a strategy per request type. Hashed assets: cache first. HTML navigations: network first with a cached fallback. API data: usually not cached unless offline is designed. Never cache non-GET.
3. Keep the worker script URL stable and make sure the server does not serve it with long caching.
4. Version cache names, and delete only your own old caches during `activate`.
5. Understand that a new worker waits until old tabs close. Either leave that, or show an update available prompt; on accept send a message that calls `skipWaiting`, then reload once on `controllerchange`.
6. Check for updates on app focus or an interval for long-lived tabs.
7. Keep previous hashed assets on the server for a while so old tabs can still load them.
8. Prepare a kill switch: a replacement worker at the same URL that clears caches and unregisters.
9. Test the upgrade from the currently deployed version to the new one, with two tabs open.

## Watch out for
- Calling `skipWaiting` unconditionally can run old page code against new cached files.
- Reloading without asking can discard unsaved input.
- Deleting the worker file from the server does not promptly rescue every installed client; ship the kill switch instead.
- One failed URL in `cache.addAll` fails the whole install.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
An old open tab learns of the new version, accepting it loads the new build exactly once without errors, offline behaviour matches the strategy table, and the kill switch has been tried.
