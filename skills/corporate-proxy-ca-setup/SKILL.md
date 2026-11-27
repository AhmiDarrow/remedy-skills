---
name: corporate-proxy-ca-setup
version: 1.0.0
description: >
  Configure developer tools to work behind a corporate proxy or TLS inspection certificate without disabling verification. Use when git, npm, pip or curl fail with certificate errors.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - environment
  - networking
  - security
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
metadata:
  source: library
  library_id: corporate-proxy-ca-setup
  official: true
  domain: tooling
  security_flags: []
---

# Corporate Proxy Ca Setup

## When to use
Downloads work in the browser but fail in command line tools on a managed network. Use only certificates and proxies the organization has provided.
## Steps
1. Capture the exact error per tool. Distinguish DNS failure, connection refused, proxy 407 and untrusted issuer.
2. Inspect the presented chain with `curl -v` or `openssl s_client -connect host:443 -showcerts`, using `-proxy` where the installed version supports it.
3. If the issuer is an internal authority, get its certificate from IT or the managed OS trust store. Verify the fingerprint through that channel; do not just trust whatever the connection presents.
4. Export it as PEM.
5. Set proxy variables `HTTPS_PROXY`, `HTTP_PROXY` and `NO_PROXY`, noting some tools read lowercase forms.
6. Configure trust per tool, since they keep separate stores: Git `http.sslCAInfo` or the OS backend on Windows; Node `NODE_EXTRA_CA_CERTS`; pip's `cert` setting; Java `keytool` import into the truststore actually used; containers need it added at image build. Show each trust-store or config change and get approval before applying it, noting how to undo it.
7. Where a variable replaces the bundle instead of extending it (as `SSL_CERT_FILE` and `REQUESTS_CA_BUNDLE` can), provide a bundle holding public roots plus the internal one.
8. Test each tool with one real fetch.
## Watch out for
- `strict-ssl=false`, `GIT_SSL_NO_VERIFY` or `curl -k` turn off protection; do not use them as a fix.
- Proxy URLs with passwords end up in config files and shell history; the user enters credentials into an approved helper.
- Certificates rotate; document where it came from.
- Keep internal certificates and proxy hostnames out of public repositories.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each needed tool fetches successfully with verification on, and the configuration and certificate source are written down locally.
