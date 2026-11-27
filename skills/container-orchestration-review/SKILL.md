---
name: container-orchestration-review
version: 1.0.1
description: >
  Review Kubernetes workload manifests before deployment for rollout safety, probes, disruption handling and security settings. Use when checking a Deployment, Helm chart or manifest change.
author: Remedy Official
license: Apache-2.0
tags:
  - k8s
  - devops
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: container-orchestration-review
  official: true
  security_flags: []
---

# Container Orchestration Review

## When to use
Manifests are about to be applied or are being reviewed.

## Steps
1. Review the rendered output, using `helm template` or `kubectl kustomize` with the values for the target environment. Rendering can include secret values, so do not paste them.
2. If authorised cluster access exists, run read-only checks: `kubectl diff` and `kubectl apply --dry-run=server`. Confirm the context first.
3. Check identity: selectors match pod labels and no other workload's, Service target ports match, and no immutable field such as a Deployment selector changes.
4. Check images use a fixed version or digest, not `latest`.
5. Check rollout: replicas, `maxUnavailable` and `maxSurge` against spare capacity, readiness gating, and whether old and new versions can run together with the same schema and messages.
6. Check probes: readiness reflects ability to serve, liveness does not depend on external services, and slow starters have a startup probe.
7. Check termination: grace period covers draining plus any `preStop` delay.
8. Check availability: replica spread across nodes or zones, and a PodDisruptionBudget that protects the service without blocking every node drain. If an autoscaler manages replicas, the manifest should not keep resetting them.
9. Check requests and limits are present and plausible.
10. Check security: non-root, `allowPrivilegeEscalation: false`, capabilities dropped, `RuntimeDefault` seccomp, no unneeded privileged mode, host namespaces or host paths, no unused service account token, and no plaintext secrets in Git. Base64 is not encryption.

## Watch out for
- A changed ConfigMap or Secret not restarting pods, or reaching some only after a later restart.
- A single replica with a budget requiring one available, which blocks drains.
- Reviewing templates while environment values override the safe defaults.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Findings cite the rendered object and field with severity and fix, checks not possible without the cluster are listed, and nothing was applied.
