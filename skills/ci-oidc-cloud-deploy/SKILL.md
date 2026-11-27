---
name: ci-oidc-cloud-deploy
version: 1.0.0
description: >
  Replace long-lived cloud keys stored in CI with short-lived federated identity tokens scoped to one repository and environment. Use when a pipeline deploys with static access keys.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - ci
  - cloud
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - web.fetch
metadata:
  source: library
  library_id: ci-oidc-cloud-deploy
  official: true
  domain: security
  security_flags: []
---

# Ci Oidc Cloud Deploy

## When to use
A deploy job authenticates with an access key or service account file saved as a CI secret.

## Steps
1. Inventory every static cloud credential the pipelines use, which jobs read it, and what permissions it holds. Cloud audit logs show what it really calls.
2. Read the current federation guide for your CI system and cloud with `web.fetch`; claim formats differ between them.
3. Register the CI system's OIDC issuer as a trusted identity provider in the cloud account.
4. Create one role per environment. In its trust policy, require the audience and match the subject claim exactly to the repository plus a protected branch, tag or deployment environment.
5. Grant each role only the actions seen in step 1 that the deploy needs.
6. Give only the deploy job permission to request a token (on GitHub Actions that is `permissions: id-token: write`), and exchange it with the provider's maintained login step.
7. Protect the matched environment with required reviewers or branch rules, since the trust policy is only as strong as who can run that ref.
8. Run a deploy, then test the negative case: a job from another branch must be refused.
9. After the owner agrees, disable the old key, watch for failures, then delete it.

## Watch out for
- A wildcard subject such as the whole organisation lets any repository in it assume the role. Some setups check only the audience, which lets other tenants of the same issuer in.
- Pull request runs have a different subject than branch pushes. Do not loosen the pattern to make them deploy.
- Deleting the key first can strand an unnoticed cron job or script that shared it. Check last-used data.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Deploys succeed with short-lived credentials, a run from an unauthorised ref is denied, and the static key is disabled.
