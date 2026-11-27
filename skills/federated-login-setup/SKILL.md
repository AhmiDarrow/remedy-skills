---
name: federated-login-setup
version: 1.0.1
description: >
  Configure an OAuth 2 or OpenID Connect client correctly: flow choice, PKCE, redirect URIs, ID token checks, account linking and token storage. Use when adding "sign in with" a provider or connecting to an OAuth API.
author: Remedy Official
license: Apache-2.0
tags:
  - auth
  - security
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - web.search
  - web.fetch
metadata:
  source: library
  library_id: federated-login-setup
  official: true
  security_flags: []
---

# Federated Login Setup

## When to use
You are building the client side of a new OAuth or OIDC integration. For auditing an existing login and session system, use a review skill.

## Steps
1. Separate the goals: OIDC to sign a user in, OAuth to call an API. An access token is not proof of who logged in.
2. Classify the client. A server app is confidential and keeps a secret server-side. Browser, mobile, desktop and CLI apps are public and cannot keep one.
3. Use the authorization code flow with PKCE (S256) for every client type. Do not use the implicit or password grants. For devices without a browser use the device flow.
4. Read the provider's discovery document and current docs for endpoints, scopes and quirks. Register exact redirect URIs per environment, no wildcards. Native apps use the system browser with a loopback or app-claimed redirect, not an embedded web view.
5. Bind each request to the user's session with a one-time `state`, and for OIDC a `nonce`. With several providers, record which one each request went to and check it on return to avoid mix-up attacks.
6. Validate the ID token with a maintained library: signature from the provider's keys with an allowed algorithm list, `iss`, `aud`, `exp` and `nonce`.
7. Key accounts on `iss` plus `sub`. Do not auto-link to an existing account just because the email matches; require the user to prove control of both.
8. Request minimal scopes. Keep tokens server-side where possible, giving a browser only an HttpOnly session cookie. Store refresh tokens encrypted or in the OS keychain, handle rotation and revocation, and make logout end your own session.
9. Test a cancelled consent, wrong state, reused code, expired token and revoked grant.

## Watch out for
- A client secret shipped in a mobile app or bundle is public.
- Tokens or codes in logs, analytics or referrer headers can be replayed.
- Concurrent refresh calls can trip rotation reuse detection and sign users out.
- The user types provider passwords and secrets; keep secrets out of the repository.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A real sign-in works against a test registration, the failure cases are rejected, and redirect URIs, scopes and token storage are documented.
