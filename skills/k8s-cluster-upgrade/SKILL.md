---
name: k8s-cluster-upgrade
version: 1.0.0
description: >
  Upgrade a Kubernetes cluster one minor version at a time with deprecated API checks, add-on compatibility and safe node draining. Use before upgrading any cluster that runs real workloads.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - kubernetes
  - upgrade
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - web.fetch
  - todo
metadata:
  source: library
  library_id: k8s-cluster-upgrade
  official: true
  domain: ops
  security_flags: []
---

# K8S Cluster Upgrade

## When to use
A cluster is falling behind supported versions or a provider has announced a forced upgrade.

## Steps
1. Record current control plane, node, and add-on versions: network plugin, DNS, ingress, storage drivers, admission webhooks and operators.
2. Fetch the release notes, API deprecation guide and version skew policy for the target version. Do not upgrade the control plane across more than one minor at a time.
3. Find removed APIs in Git manifests, chart templates and live clients. The API server metric `apiserver_requested_deprecated_apis` shows deprecated APIs still being called.
4. Check each add-on's compatibility table and upgrade in the order it requires.
5. Back up cluster state (an etcd snapshot if you run the control plane) plus persistent data, and know that control plane downgrade is generally not supported.
6. Rehearse on a non-production cluster with the same add-ons.
7. Check PodDisruptionBudgets: a budget allowing zero disruptions blocks drains.
8. Upgrade the control plane, verify, then nodes in small batches: `kubectl cordon`, then `kubectl drain <node> --ignore-daemonsets`, upgrade or replace, wait Ready, uncordon.
9. After each batch check pending pods, restarts, DNS resolution and ingress traffic.

## Watch out for
- `--delete-emptydir-data` destroys data in emptyDir volumes; read what drain refuses before adding it.
- A fail-closed admission webhook whose pods are being drained can block all new pods.
- Draining pods tied to local disks may leave them unschedulable elsewhere.
- Force-deleting to get past a budget can break quorum in a database.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All nodes report the target version and Ready, add-ons are on supported versions, and workload health checks match the pre-upgrade baseline.
