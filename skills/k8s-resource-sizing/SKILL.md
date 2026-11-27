---
name: k8s-resource-sizing
version: 1.0.0
description: >
  Set Kubernetes CPU and memory requests and limits from observed usage, covering throttling, OOM kills and eviction order. Use when workloads are throttled, OOM-killed or badly over-provisioned.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - kubernetes
  - capacity
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: k8s-resource-sizing
  official: true
  domain: ops
  security_flags: []
---

# K8S Resource Sizing

## When to use
Requests were guessed, nodes look full while idle, or pods are killed or slow under load.

## Steps
1. Collect per-container memory working set and CPU usage over a period that includes peaks, deploys and batch jobs, at least a week where possible. `kubectl top` is a single moment and not enough.
2. Collect CPU throttling counters and restart reasons.
3. Set the memory request near high-percentile steady usage and the limit above the observed peak including startup. Memory is not compressible: crossing the limit kills the container.
4. Set the CPU request to what the workload needs under contention, since it determines its share. Add a CPU limit only if policy or noisy-neighbour control requires it; limits throttle even when the node has idle CPU.
5. Check runtime settings follow the container limits: JVM heap flags, Node's old-space size, Go's `GOMAXPROCS` and `GOMEMLIMIT`, worker counts derived from host cores.
6. Decide the QoS class deliberately. Requests equal to limits for both resources on every container gives Guaranteed, which is evicted last.
7. If a horizontal autoscaler targets CPU utilisation, remember the percentage is of the request, so changing requests changes scaling behaviour. Recalculate the target.
8. Roll out one workload at a time and compare latency, throttling and kills afterwards.

## Watch out for
- Averages hide the spikes that cause OOM kills.
- Sidecars and init containers count toward what the pod needs to be scheduled.
- Memory-backed emptyDir volumes count against memory.
- Cutting requests across a cluster at once can overpack nodes and trigger evictions.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each changed container has values traceable to recorded usage, and a full peak period passes without new OOM kills or worse latency.
