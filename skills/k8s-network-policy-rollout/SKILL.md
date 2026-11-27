---
name: k8s-network-policy-rollout
version: 1.0.0
description: >
  Introduce default-deny Kubernetes network policies namespace by namespace without cutting off DNS or required traffic. Use when every pod can currently reach every other pod.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - kubernetes
  - networking
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - grep
metadata:
  source: library
  library_id: k8s-network-policy-rollout
  official: true
  domain: security
  security_flags: []
---

# K8S Network Policy Rollout

## When to use
A cluster has flat pod networking and you need to limit lateral movement.

## Steps
1. Confirm the network plugin enforces NetworkPolicy. Without that, policies are accepted and silently do nothing. Prove it with a throwaway namespace and a deny rule.
2. Map real flows for one namespace from flow logs, mesh telemetry or application config. Include scrapers, ingress controllers, webhooks, backups, batch jobs and external APIs.
3. Write allow policies first, selecting pods by stable labels.
4. Include DNS egress to the cluster DNS pods on UDP and TCP 53. Select its namespace by the `kubernetes.io/metadata.name` label, and check whether the cluster uses a node-local DNS cache that needs a different rule.
5. Add the default deny: an empty `podSelector` with `policyTypes` Ingress and Egress and no rules.
6. Apply in a test environment, then exercise every flow, including scheduled ones.
7. Test denial too: from an unrelated temporary pod, a connection to the protected service must time out.
8. Apply to production one namespace at a time, with the delete command ready, and watch errors through at least one cron cycle.

## Watch out for
- Policies are additive allows; there is no deny rule that overrides another policy.
- In a `from` or `to` list, `namespaceSelector` and `podSelector` in one item mean both must match; as two separate items either one matches, which is far wider.
- Both sides need permission: egress on the source and ingress on the destination.
- Established connections may survive a new policy, so failures can appear only after reconnect.
- IP rules for external services break when the provider changes addresses.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each protected namespace has a default deny, required flows including DNS and scheduled jobs succeed, and an unlisted connection is shown to fail.
