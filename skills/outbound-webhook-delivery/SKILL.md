---
name: outbound-webhook-delivery
version: 1.0.0
description: >
  Build the sending side of webhooks with signed payloads, retries, delivery logs and protection against internal-network targets. Use when your service must notify customer URLs of events.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - webhooks
  - api
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: outbound-webhook-delivery
  official: true
  domain: backend
  security_flags: []
---

# Outbound Webhook Delivery

## When to use
Your application needs to push events to URLs that users or partners register.

## Steps
1. Never deliver inside the request that caused the event. Record the event in the same transaction as the change, then let a worker deliver it.
2. Define the envelope: unique event id (stable across retries), type, creation time, schema version and data.
3. Sign `timestamp + "." + raw body` with HMAC-SHA256 using a per-endpoint secret; send the timestamp and signature in headers. Allow two active secrets so they can rotate.
4. Guard against server-side request forgery: require HTTPS, resolve the host, reject loopback, private, link-local and metadata ranges for IPv4 and IPv6, connect to the address you validated, and do not follow redirects.
5. Use a short timeout and cap how much response body you read. Treat any 2xx as delivered.
6. Retry with growing, jittered delays over a documented window, then mark the delivery failed.
7. Isolate endpoints: limit concurrency per destination so one slow receiver cannot starve the rest.
8. Store each attempt with time, status, duration and a truncated response; offer manual redelivery that keeps the same event id.
9. After sustained failure, disable the endpoint and tell its owner.
10. Document that delivery is at least once and may arrive out of order, so receivers must deduplicate by event id.

## Watch out for
- Validating the hostname and then letting the HTTP client resolve it again permits DNS rebinding.
- Signing a re-serialized object can differ byte for byte from what was sent; sign the exact bytes.
- Sending full records leaks data to a mistyped URL. Consider sending ids and letting the receiver fetch.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A local test receiver verifies the signature, a failing receiver produces logged retries then a failed state, and a private-address URL is refused.
