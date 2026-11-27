---
name: android-process-death-state
version: 1.0.0
description: >
  Fix Android apps that lose input or crash after being killed in the background, by saving and restoring the right state. Use when returning to an app resets screens or throws null errors.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - android
  - state
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: android-process-death-state
  official: true
  domain: frontend
  security_flags: []
---

# Android Process Death State

## When to use
Users switch to another app and come back to a blank form, wrong screen or crash that developers cannot reproduce.

## Steps
1. Reproduce deliberately: put the app in the background, run `adb shell am kill <package>`, then reopen from recents. The developer option Don't keep activities tests activity recreation only, not loss of static and singleton state.
2. Walk each screen's flow this way and record what is lost or crashes.
3. Classify state: persistent data in database or datastore; small UI state (typed text, selected id, scroll, step) in saved instance state; derived or large data reloaded from its source.
4. In view models use `SavedStateHandle`; in Compose use `rememberSaveable`, with a custom `Saver` where needed. Plain `remember` and view model fields do not survive process death.
5. Save ids, not whole objects or lists, since the saved bundle has tight size limits and overflow crashes with `TransactionTooLargeException`.
6. Remove assumptions that an earlier screen ran: singletons filled at login, in-memory caches, static fields. Each destination must load what it needs from its arguments.
7. Persist long drafts to disk as the user types.
8. Handle in-progress work using WorkManager or an idempotent resume rather than assuming it finished.
9. Repeat the kill test on every screen, and also rotate.

## Watch out for
- Swiping the app away from recents is not the same scenario; saved state is discarded.
- Rotation passing proves little, because view models survive rotation but not process death.
- Restored navigation can open a screen after the session expired; check auth there.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
After a forced background kill, each tested screen returns with its input and position intact or reloads cleanly, with no crash.
