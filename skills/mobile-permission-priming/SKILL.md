---
name: mobile-permission-priming
version: 1.0.0
description: >
  Request mobile permissions such as notifications, camera, photos and location at the right moment with denial recovery. Use when adding a permission or when grant rates are poor.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - mobile
  - ux
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: mobile-permission-priming
  official: true
  domain: frontend
  security_flags: []
---

# Mobile Permission Priming

## When to use
An app prompts at first launch, crashes on missing permission, or dead-ends after a refusal.

## Steps
1. For each permission name the feature it serves and ask whether it is needed at all. System photo pickers, share sheets and one-time location often avoid broad access.
2. Check manifest and `Info.plist` entries, including those merged in by libraries. iOS usage description strings must state a specific reason; missing ones crash at the request.
3. Ask in context, when the user taps the feature. Where the reason is not obvious, show your own short explanation first with a way to decline that does not spend the system prompt.
4. Handle every status: not determined, granted, limited or partial (selected photos, approximate location), denied, restricted by policy.
5. On Android 13 and later notifications need the `POST_NOTIFICATIONS` runtime permission; create channels with sensible categories. Use `shouldShowRequestPermissionRationale`, remembering it is also false before the first request.
6. On iOS the notification prompt is effectively one chance; consider provisional authorization for quiet delivery.
7. After denial keep the rest of the app usable, explain what is unavailable, and link to system settings only when the user tries the feature.
8. Recheck status when the app returns to the foreground, because users change settings or the system revokes unused grants.
9. Test fresh install, deny, deny twice, grant later and revoke while backgrounded.

## Watch out for
- A pre-prompt styled to imitate the system dialog, or blocking use until granted, risks store rejection.
- Requesting several permissions in a row gets them refused together.
- A push token or permission can change; re-register rather than caching once.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every status for each permission has a working screen, no prompt appears before its feature is requested, and the listed install and revoke scenarios pass.
