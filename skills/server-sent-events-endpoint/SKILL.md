---
name: server-sent-events-endpoint
version: 1.0.0
description: >
  Stream server-to-client updates with Server-Sent Events that survive proxies, reconnects and many open connections. Use when building live progress, feeds or token-by-token output over HTTP.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - streaming
  - http
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: server-sent-events-endpoint
  official: true
  domain: backend
  security_flags: []
---

# Server Sent Events Endpoint

## When to use
Data flows mainly from server to client, such as progress, notifications or incremental text, and a full bidirectional socket is unnecessary.

## Steps
1. Respond with `Content-Type: text/event-stream` and `Cache-Control: no-cache`, and flush after each event.
2. Frame events correctly: `event:`, `id:` and `data:` lines ending with a blank line. A payload containing newlines needs one `data:` line per line, or send single-line JSON.
3. Give each event a monotonic id. On reconnect the browser's `EventSource` sends `Last-Event-ID`; replay from a bounded buffer or send a "resync" event when the gap is too old.
4. Send a comment line (`: ping`) every 15-30 s so idle timeouts do not close the stream.
5. Disable buffering and compression along the path. For nginx, turn off `proxy_buffering` for the route or send `X-Accel-Buffering: no`.
6. Detect client disconnect and release subscriptions, timers and upstream requests.
7. Send an explicit final event for finite streams and have the client call `close()`; otherwise `EventSource` reconnects and may rerun the work.
8. Plan auth: `EventSource` cannot set custom headers, so use cookies with origin checks, or read the stream with `fetch`. Do not put long-lived tokens in the URL.
9. Verify with `curl -N` against the production-like front door and watch events arrive one at a time.

## Watch out for
- Over HTTP/1.1 browsers cap connections per origin at about six, so several tabs can starve the site. Use HTTP/2 or share one stream.
- Once headers are sent the status cannot change; report mid-stream errors as an event type the client handles.
- Thread-per-request servers run out of workers with idle streams.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Events arrive incrementally through the proxy, a dropped connection resumes without loss or duplication, and disconnecting frees server resources.
