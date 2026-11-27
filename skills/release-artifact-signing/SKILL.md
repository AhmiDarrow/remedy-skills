---
name: release-artifact-signing
version: 1.0.0
description: >
  Sign release artifacts and images, attach provenance, and enforce verification where they are consumed. Use when users or deploy systems cannot tell whether a download is genuine.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - release
  - supply-chain
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - web.fetch
metadata:
  source: library
  library_id: release-artifact-signing
  official: true
  domain: security
  security_flags: []
---

# Release Artifact Signing

## When to use
You publish binaries, packages or container images that others install or that your own infrastructure deploys.

## Steps
1. List every published artifact type and every place that consumes it. Signing without a verifying consumer protects nothing.
2. Pick the mechanism each platform checks: OS code signing for Windows and macOS installers (macOS also needs notarization for normal downloads), repository signing for Linux packages, and Sigstore `cosign` or an equivalent for images and generic files.
3. Decide where keys live. Prefer keyless identity-based signing from CI or a hardware or managed key service over a private key file in CI secrets.
4. Sign in a release job that runs only from protected tags and does not execute unreviewed code.
5. Sign images by digest, not tag. Generate a SHA-256 manifest for file downloads and sign the manifest.
6. Attach build provenance naming the source repository, commit and workflow.
7. Add verification at consumption. With keyless `cosign verify`, require the exact `--certificate-identity` and `--certificate-oidc-issuer`.
8. Test refusal: modify one byte, and sign with a different identity. Both must fail.
9. Document for users how to verify, and write down what to do if the key or signing workflow is compromised.

## Watch out for
- "Signature valid" without checking who signed accepts anyone's signature.
- Checksums hosted next to the download catch corruption, not an attacker who can replace both.
- Keyless signing records identity data in a public transparency log; check that is acceptable for private repository names.
- Confirm flags against the installed tool version before scripting them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A genuine release verifies against a pinned identity or key, tampered and wrongly signed copies are rejected, and consumers run that check.
