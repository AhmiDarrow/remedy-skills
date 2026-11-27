---
name: cors-review
version: 1.0.1
description: >
  Review CORS settings for reflected or over-broad origins, credential exposure, preflight and caching mistakes. Use when auditing cross-origin access on your API or fixing a CORS error without opening it to everyone.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - web
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: cors-review
  official: true
  security_flags: []
---

# Cors Review

## When to use
An API or site you own sets CORS headers, or a browser is blocking a legitimate frontend.

## Steps
1. Find every layer that sets `Access-Control-*`: framework middleware, routes, reverse proxy, gateway, CDN and storage bucket. Two layers can add duplicate headers, which browsers reject.
2. List required frontend origins per environment (scheme, host, port) and whether each request uses cookies, HTTP auth or an `Authorization` header.
3. Flag any code that echoes the request `Origin` without an exact allowlist, especially with `Access-Control-Allow-Credentials: true`. Literal `*` fails for credentialed requests, which tempts developers into reflection.
4. Test matching logic: unanchored regex, unescaped dots, prefix or suffix checks that accept `app.example.com.attacker.example` or `evilexample.com`, trusted `null`, any-subdomain rules and plain `http` origins.
5. Keep development origins out of production. Even `*` without credentials is unsafe for data protected only by network position, such as internal services.
6. Allow only needed methods and request headers; expose only needed response headers. List `Authorization` explicitly; the wildcard does not cover it.
7. Make preflight `OPTIONS` succeed without authentication, since it carries no credentials, while the real request stays protected.
8. When the allowed origin varies, send `Vary: Origin` and check CDN cache behaviour.
9. Verify with `curl -i` (use `curl.exe` in PowerShell) against a system you may test, sending trusted, hostile, lookalike and `null` `Origin` values, including preflight with `Access-Control-Request-Method`. Then confirm the real frontend in a browser.

## Watch out for
- CORS is not authentication or CSRF protection. It controls reading responses in browsers; some cross-origin requests are still sent, and non-browser clients ignore it.
- WebSocket handshakes are not protected by CORS; validate `Origin` on the server.
- `no-cors` mode does not fix an error; the response becomes unreadable.
- Fix error responses too, or real failures appear as CORS errors.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Only listed origins receive allow headers, hostile and lookalike origins do not, preflight and the real frontend work, and untested layers are named.
