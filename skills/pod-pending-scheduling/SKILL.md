---
name: pod-pending-scheduling
version: 1.0.0
description: >
  Diagnose Kubernetes pods stuck in Pending by reading scheduler events against node capacity, taints, affinity and volumes. Use when pods are created but never get scheduled or started.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - kubernetes
  - scheduling
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: pod-pending-scheduling
  official: true
  domain: ops
  security_flags: []
---

# Pod Pending Scheduling

## When to use
Pods stay Pending or ContainerCreating and the application never runs.

## Steps
1. Run `kubectl describe pod` and check whether a node is assigned. No node means a scheduling problem; an assigned node means volume, network or image setup on that node.
2. For unscheduled pods, break the FailedScheduling message into its per-reason node counts; the nodes may each fail for a different reason.
3. Insufficient cpu or memory: compare the pod's requests with Allocatable and "Allocated resources" in `kubectl describe node`. Scheduling uses requests, not live usage.
4. Taints: list node taints and the pod's tolerations. A toleration permits a node but does not attract the pod to it.
5. Affinity, nodeSelector and topology spread: check the labels really exist on nodes. Required anti-affinity with more replicas than hosts can never be satisfied.
6. Volumes: run `kubectl get pvc` and describe it. Check the storage class, and whether a zonal volume restricts the pod to a zone with no room.
7. Also check namespace ResourceQuota (its failures appear on the ReplicaSet events, with no pod created) and per-node pod limits.
8. If an autoscaler should add nodes, read its events for why it declined: group at maximum, or no node type can fit the pod.
9. For node-assigned pods, follow the image pull, mount or network plugin event.

## Watch out for
- One request larger than any node's allocatable stays Pending however many nodes of that size are added.
- Removing a taint to get one pod running can let all workloads onto reserved or unhealthy nodes.
- Deleting a PVC to unstick a pod can delete the underlying data, depending on the reclaim policy.
- Events expire after a while; an old Pending pod may show none until something retriggers scheduling.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The pod is Running and Ready, or the exact blocking constraint is reported with the options to change the pod or the cluster.
