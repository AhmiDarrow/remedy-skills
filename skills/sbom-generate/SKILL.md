---
name: sbom-generate
version: 1.0.1
description: >
  Generate a software bill of materials in CycloneDX or SPDX from the right source, then check it is complete. Use when a customer, release process or audit asks for an SBOM.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - supply-chain
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - glob
metadata:
  source: library
  library_id: sbom-generate
  official: true
  security_flags: []
---

# Sbom Generate

## When to use
You must list the components in a specific release or artifact.

## Steps
1. Ask what the SBOM must describe (source tree, build, container image or installer), the required format and version, and any required fields from the recipient.
2. Prefer scanning what ships. A source lockfile scan misses OS packages and copied binaries; an image scan may miss bundled front-end or statically linked code. Combine or supply both if needed.
3. Check installed tools: `syft` (directories and images), `trivy` with CycloneDX or SPDX output, `npm sbom --sbom-format cyclonedx` on npm versions that include it, or ecosystem plugins for Cargo, Python, Maven or Gradle. Check each tool's help for output flags. Install only with approval.
4. Build from locked dependencies at the release commit or by image digest. Record whether development dependencies are included.
5. Write to the user's path with the product name and version in the filename.
6. Validate against the schema with an available validator.
7. Check completeness: compare component count and a sample of direct and transitive dependencies with the lockfiles; look for versions, package URLs, licences, hashes and dependency relationships. List vendored, copied and manually downloaded code and add or disclose it.
8. Record tool, version and exact command in the build script, so each release regenerates it.

## Watch out for
- An SBOM is not a vulnerability scan or a licence review, and unknown licence fields stay unknown.
- A stale SBOM attached to a new build is misleading.
- It can reveal internal package names and paths; review before sharing outside.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The file validates, is tied to an exact commit or digest, the regeneration command works, and known gaps are written next to it.
