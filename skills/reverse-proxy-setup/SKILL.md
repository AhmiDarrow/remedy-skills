---
name: reverse-proxy-setup
version: 1.0.0
description: >
  Configure a reverse proxy in front of web apps with correct forwarded headers, WebSocket support, timeouts, limits and TLS. Use when publishing one or more services behind nginx, Caddy or similar.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - networking
  - selfhost
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
metadata:
  source: library
  library_id: reverse-proxy-setup
  official: true
  domain: ops
  security_flags: []
---

# Reverse Proxy Setup

## When to use
One entry point should serve and protect backends.

## Steps
1. List each hostname, upstream address, protocol, authentication need, upload size and any long-lived connections.
2. Bind backends to loopback or a private network so the proxy cannot be bypassed.
3. Define explicit server blocks plus a default that rejects unknown hostnames.
4. Pass the original Host and protocol, and set forwarded-for headers. At the outermost proxy, overwrite client-supplied values rather than appending trust to them.
5. Configure the application to trust forwarded headers only from the proxy's address.
6. Enable WebSocket forwarding where needed. In nginx this requires `proxy_http_version 1.1` and passing the Upgrade and Connection headers; Caddy handles it by default.
7. Set body size, connect and read timeouts per application; turn off response buffering for server-sent events.
8. Terminate TLS with automated renewal, redirect HTTP, and add HSTS only after HTTPS works everywhere it will apply.
9. Validate (`nginx -t` or `caddy validate`), reload rather than restart, and test each host, the unknown-host case, a large upload and a long connection.

## Watch out for
- In nginx, a trailing slash or URI on `proxy_pass` changes how the path is rewritten.
- nginx `add_header` in an inner block replaces the inherited set.
- Putting authentication on the proxy is useless if the backend port is still reachable.
- Published container ports can bypass host firewall rules managed by tools such as ufw.
- Access logs may record tokens in query strings.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each hostname reaches only its intended app, direct backend access from outside fails, and logs show the true client address.
