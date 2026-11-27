---
name: http-debugging
version: 1.0.1
description: >
  Debug a failing HTTP request layer by layer with curl, comparing against a working case. Use when a call returns unexpected statuses, hangs, redirects wrongly or works in one client only.
author: Remedy Official
license: Apache-2.0
tags:
  - network
  - debug
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: http-debugging
  official: true
  security_flags: []
---

# Http Debugging

## When to use
An HTTP request misbehaves and the cause is unclear. In Windows PowerShell call `curl.exe`, since `curl` may be an alias.

## Steps
1. Capture the exact failing method, URL, headers, body, time and client. Replace credentials with placeholders in anything shared.
2. Reproduce with `curl -v`, reading secrets from environment variables. Verbose output prints authorization headers and cookies, so redact before showing it. Replay writes only against safe targets or with approval.
3. Locate the failing layer: name resolution, TCP connect, TLS, request, server wait or body. A `-w` format with the `time_` variables shows where time goes.
4. Test routes with `--resolve` to hit one server while keeping the correct host name. Check proxy variables and compare with `--noproxy`, plus IPv4 against IPv6.
5. Find who answered: application, proxy, CDN or firewall, using response headers, error page and request ID, then check that component's logs.
6. Follow redirects one at a time. Check scheme, host, method changes and dropped authorization.
7. Diff against a working request one difference at a time: path encoding, content type, body bytes, cookies, auth audience and expiry, clock skew, HTTP version.
8. If only a browser fails, check CORS preflight, cookie attributes and the network panel.
9. State root cause with evidence, apply or propose the fix, and rerun the original case.

## Watch out for
- `-k` may help isolate a certificate problem but is never the fix.
- `-I` sends HEAD, which servers may treat differently from GET.
- A gateway 502 or 504 describes its upstream connection, not necessarily your request.
- HAR files and traces contain live session tokens.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing layer and cause are shown by evidence and the original request behaves correctly, or the next owner has a redacted reproduction with timestamps and request IDs.
