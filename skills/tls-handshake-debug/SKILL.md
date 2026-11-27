---
name: tls-handshake-debug
version: 1.0.0
description: >
  Diagnose TLS certificate and handshake errors by inspecting the served chain, names, SNI, protocol versions and client trust store. Use when HTTPS or another TLS client refuses to connect.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - tls
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: tls-handshake-debug
  official: true
  domain: ops
  security_flags: []
---

# Tls Handshake Debug

## When to use
Errors such as unknown issuer, name mismatch, expired certificate or handshake failure.

## Steps
1. Capture the exact error, client software, hostname and port. Confirm DNS and which IP the client reaches; one load balancer node may differ.
2. Connect with `openssl s_client -connect <ip>:443 -servername <host> -showcerts`. Without correct SNI you may be shown a different certificate.
3. Check each presented certificate with `openssl x509 -noout -subject -issuer -dates`, and print the leaf with `-text` to read Subject Alternative Names.
4. Confirm the hostname is covered. A wildcard matches one label only.
5. Check the server sends the leaf plus required intermediates. Browsers may hide a missing intermediate that command-line and library clients reject.
6. Test verification with `-verify_return_error -verify_hostname <host>`, noting which trust store the failing runtime uses: OS, Java keystore, a bundled CA file or a container image.
7. Check the client clock.
8. For handshake alerts before certificates, compare supported protocol versions and ciphers, ALPN, and whether the server requires a client certificate.
9. Compare the issuer with the expected one. An unexpected issuer suggests an intercepting proxy or the wrong endpoint.
10. Fix and retest with the original client.

## Watch out for
- Disabling verification (`curl -k` or an equivalent setting) is a diagnostic at most, never the fix.
- Renewed files do nothing until the serving process reloads them.
- Private keys must not be pasted into chats or online checkers.
- STARTTLS services need the matching `-starttls` option.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing check is named with evidence, and the original client connects with verification enabled.
