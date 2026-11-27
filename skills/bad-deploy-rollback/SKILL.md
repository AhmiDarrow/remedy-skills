---
name: bad-deploy-rollback
version: 1.0.0
description: >
  Decide between rolling back and rolling forward after a harmful release, execute safely and verify recovery. Use when errors or user reports start right after a deployment.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - deploy
  - incident
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - owner.notify
metadata:
  source: library
  library_id: bad-deploy-rollback
  official: true
  domain: ops
  security_flags: []
---

# Bad Deploy Rollback

## When to use
A release is live, something is broken, and the timing points at it.

## Steps
1. Confirm the correlation: compare error onset with deploy time, check whether only new-version instances fail, and look for other changes in that window (config, flags, infrastructure, dependency outage).
2. List what shipped: code, schema migrations, config, flags, queued message formats.
3. If a feature flag can disable the faulty path, turn that off first; it is the smallest reversal.
4. Check whether the previous version can run against current data. Dropped or renamed columns, new enum values and new serialized formats are the usual blockers. If it cannot, plan a forward fix instead of rolling back into a worse failure.
5. Tell the owner the chosen action and expected effect, and get a go-ahead for production.
6. Redeploy the previous known artifact by digest or revision (for a Kubernetes Deployment, `kubectl rollout history deployment/<name> -n <ns>` then `kubectl rollout undo deployment/<name> -n <ns> --to-revision=N`). Do not rebuild.
7. Disable automatic redeploy, or revert in Git, so a pipeline or GitOps controller does not restore the bad version.
8. Verify with the same signals that showed the fault, and check backlogs, dead-letter queues and records written incorrectly while it was live.

## Watch out for
- `rollout undo` restores the pod template only, not changed ConfigMaps, Secrets or database state.
- Running a down migration under pressure can destroy data written since the release. Prefer leaving additive schema in place.
- Restarting everything before saving logs or a sample bad request loses the evidence needed for the fix.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
User-facing error signals are back at their earlier baseline, redeploy of the bad version is blocked, and damaged data or backlog is either repaired or listed with an owner.
