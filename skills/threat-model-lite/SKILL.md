---
name: threat-model-lite
version: 1.0.1
description: >
  Write a one-page threat model for a feature covering assets, trust boundaries, abuse cases, mitigations and accepted risk. Use when designing something that handles sensitive data, money, access or untrusted input.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - design
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: threat-model-lite
  official: true
  security_flags: []
---

# Threat Model Lite

## When to use
A feature is being designed or has just grown a new way in, and a full formal assessment is not warranted.

## Steps
1. State in two or three lines what the feature does and what is out of scope.
2. Name assets and the harm if each is read, changed, destroyed or made unavailable, including money, spend on paid services and user trust.
3. Sketch data flows from the real code or design: components, stores and third parties, marking each trust boundary where data or privilege changes hands.
4. List actors: anonymous, ordinary user acting against another, over-privileged insider, compromised dependency or integration, and automated abuse.
5. At each entry point (HTTP, jobs, queues, webhooks, files, admin tools, update channels) ask about spoofing, tampering, deniability, disclosure, denial of service and gaining privilege.
6. Write abuse cases as concrete sentences: who sends what, and what they get. "User changes the invoice ID and downloads another company's invoice."
7. Rank by plausibility and damage. For each top case name the mitigation, whether it exists (with file reference), is planned or is absent, and a test or signal that proves it.
8. Record assumptions, residual risks, who accepts each one and what change should trigger a revisit. Save it beside the design or in the repository's docs.

## Watch out for
- A list of generic threats that would fit any feature gives nobody anything to do.
- "We use TLS" and "users are authenticated" do not answer what an authenticated user can abuse.
- Marking a mitigation present without seeing it in code or configuration.
- Detailed unfixed weaknesses should not be published in a public repository.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The page fits what was built, each top abuse case has a verified or planned mitigation with an owner or an explicit acceptance, and unknowns are listed.
