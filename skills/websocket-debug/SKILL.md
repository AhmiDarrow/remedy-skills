---
name: websocket-debug
version: 1.0.1
description: >
  Diagnose WebSocket failures from handshake to disconnect: proxy upgrade, origin and auth, close codes, idle timeouts and reconnect storms. Use when sockets fail to connect, drop or reconnect in loops.
author: Remedy Official
license: Apache-2.0
tags:
  - network
  - debug
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: websocket-debug
  official: true
  security_flags: []
---

# Websocket Debug

## When to use
A real-time connection misbehaves.

## Steps
1. Record client, URL, environment, time to failure, close code and reason, and whether every user or only some are affected.
2. Capture the handshake in the browser network panel or a command-line client, redacting tokens. HTTP/1.1 success is 101. A 401 or 403 points to auth or origin; 400, 404 or 426 often to routing or missing upgrade headers; 200 means something answered as ordinary HTTP.
3. Connect directly to the app, then through each proxy. Check upgrade forwarding (nginx needs HTTP/1.1 and the Upgrade and Connection headers), path, TLS and `ws` versus `wss`.
4. Check auth: browsers cannot set arbitrary headers on WebSocket, so verify the cookie, subprotocol or short-lived ticket in use. With cookie auth the server must validate Origin. Avoid long-lived tokens in URLs.
5. Time the drops. A constant interval suggests an idle or maximum-duration timeout; compare it with each hop and send heartbeats more often than the shortest idle limit.
6. Read close codes with logs. 1006 is reported locally when no close frame arrived and gives no cause; 1009 means message too big; 1008 policy; 1011 server error.
7. With several instances, check affinity if the protocol needs it, cross-instance publishing and deploy draining.
8. Reconnect with exponential backoff, jitter and a cap; stop on auth failure, close old timers and resynchronise missed messages.
9. Reproduce a server restart and network drop to verify.

## Watch out for
- Some libraries layer their own protocol, so a plain WebSocket client cannot connect.
- An open socket can be dead without heartbeat timeouts.
- Slow consumers grow send buffers.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing hop and cause are evidenced and the connection survives the formerly failing case, or the remaining unknown has a stated capture to collect next.
