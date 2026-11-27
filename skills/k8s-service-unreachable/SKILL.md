---
name: k8s-service-unreachable
version: 1.0.0
description: >
  Trace a Kubernetes service that cannot be reached, hop by hop from pod to endpoints, service, DNS, ingress and load balancer. Use when pods look healthy but requests time out or return errors.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - kubernetes
  - networking
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: k8s-service-unreachable
  official: true
  domain: ops
  security_flags: []
---

# K8S Service Unreachable

## When to use
An application in a cluster is unreachable, from inside or outside.

## Steps
1. Record the exact failing request and error. Refused, timeout, DNS failure, 502, 503 and 404 each point to different hops.
2. Test the pod directly with `kubectl port-forward` and, from a temporary debug pod, by pod IP. Check the app listens on `0.0.0.0` or the pod address, not only loopback; port-forward succeeds even for loopback-only listeners.
3. Check the pods are Ready, then run `kubectl get endpointslices -n <ns> -l kubernetes.io/service-name=<svc>`. No ready endpoints means a selector or readiness problem.
4. Compare the Service's selector with pod labels, and `targetPort` with the container's real port or port name.
5. From the debug pod call the ClusterIP, then the DNS name `<svc>.<ns>.svc`. IP works but name fails: check cluster DNS pods, logs and egress policy.
6. Test from the same namespace as the real caller, since network policies depend on source.
7. For outside traffic, check ingress class, host and path rules, backend port, TLS secret and the ingress controller's logs for this request.
8. For a load balancer, check the assigned address, health check target and firewall rules. With `externalTrafficPolicy: Local`, nodes without a local endpoint fail health checks by design.

## Watch out for
- Ping to a ClusterIP often fails on a healthy service; test the real TCP or HTTP port.
- `containerPort` is mostly documentation and does not make the process listen there.
- A 503 from a mesh or ingress can be caused by TLS mode mismatch to the backend.
- Fixing by switching to NodePort bypasses the broken layer and may expose the app.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing hop is identified with a test that succeeds just before it and fails at it, and the original request works after the fix.
