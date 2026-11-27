---
name: cloud-iam-least-privilege
version: 1.0.0
description: >
  Reduce cloud identity permissions using last-access and audit data, staged replacement policies and a tested way back. Use when roles carry wildcard or administrator rights they do not need.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - cloud
  - access
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
metadata:
  source: library
  library_id: cloud-iam-least-privilege
  official: true
  domain: security
  security_flags: []
---

# Cloud Iam Least Privilege

## When to use
Cloud roles, service identities or user accounts have accumulated more access than their job needs.

## Steps
1. Export identities, group memberships, attached and inline policies, trust policies and access keys with last-used dates.
2. Rank by risk: internet-reachable workloads, CI roles, human admins, third-party access, then the rest.
3. For one identity, gather actions actually used over a window that includes monthly and quarterly jobs, from audit logs or the provider's access analyser. Check which data-plane events are not logged by default.
4. Look for escalation permissions: editing policies, creating keys for other identities, passing a more powerful role to compute, updating functions that run as another role.
5. Draft a policy with explicit actions and resource scopes, adding conditions where the provider supports them.
6. Test with the policy simulator if available and in a non-production account.
7. Attach the new policy, detach the old but keep its definition, and watch access-denied events.
8. Confirm a break-glass admin path, protected by strong MFA and alerted on use, before narrowing human admins. The user performs any MFA enrolment.
9. Remove unused identities by disabling first and deleting after a quiet period.

## Watch out for
- Unused during the window is not the same as unneeded; disaster recovery roles may sit idle for a year.
- Organisation guardrails, resource policies and permission boundaries also affect the result, so reading identity policies alone misleads.
- A trust policy open to a whole external account matters as much as the permissions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each reviewed identity has a narrowed policy backed by usage evidence, required workflows ran without denials, and the rollback definition is stored.
