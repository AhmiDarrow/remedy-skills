---
name: auth-session-review
version: 1.0.1
description: >
  Review login, password reset, session, JWT and OAuth code for authentication and session flaws, with evidence and fixes. Use when auditing sign-in code you own or are authorised to assess, or after changing it.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - auth
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
metadata:
  source: library
  library_id: auth-session-review
  official: true
  security_flags: []
---

# Auth Session Review

## When to use
A defensive code and configuration review of authentication in a system the user owns or may test.

## Steps
1. Map every way to obtain or restore access: password, social or enterprise login, magic link, API token, reset, email change, invite, remember-me and support override. Weak side paths defeat a strong login.
2. Passwords: require a slow salted scheme through a maintained library, preferably Argon2id (OWASP's baseline is at least 19 MiB memory, 2 iterations, parallelism 1), otherwise scrypt, bcrypt for legacy (note its 72-byte input limit) or PBKDF2 where FIPS requires it. Check current OWASP parameters and upgrade-on-login.
3. Check rate limits on login, reset, code entry and signup by account and source, without letting others lock a victim out. Compare messages and timing for account enumeration.
4. Reset and magic links: random, single-use, short-lived, stored hashed, bound to the account, with link host not taken from the request.
5. Sessions: new identifier after login and privilege change; cookies `Secure`, `HttpOnly`, suitable `SameSite` and narrow scope; idle and absolute expiry; CSRF protection on cookie-authenticated state changes.
6. Revocation: logout, password change, account disable and two-step reset must end the intended sessions and refresh tokens server-side.
7. JWT: verify signature with an algorithm allowlist fixed by the server; check `iss`, `aud`, `exp` and token type; control key lookup from `kid`; never trust decode-only calls. Refresh tokens rotate with reuse detection or are sender-constrained for public clients.
8. OAuth/OIDC: authorization code with PKCE, exact redirect URI matching, `state` bound to the browser, ID token and `nonce` validation. Link accounts by issuer plus subject, not email alone.
9. Confirm two-step cannot be skipped by calling later endpoints, and that authorization is checked server-side per request.

## Watch out for
- Reporting from a library name without reading how it is configured.
- Quoting real tokens, cookies or secrets in findings; redact them.
- Calling untested runtime behaviour confirmed.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every access path is marked reviewed or not, and each finding has `path:line`, impact, fix and confirmed or suspected status.
