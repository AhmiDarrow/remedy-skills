---
name: pod-crashloop-diagnose
version: 1.0.0
description: >
  Find why a Kubernetes pod keeps restarting using exit codes, previous logs, events and probe settings. Use when a pod shows CrashLoopBackOff or its restart count keeps climbing.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - kubernetes
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: pod-crashloop-diagnose
  official: true
  domain: ops
  security_flags: []
---

# Pod Crashloop Diagnose

## When to use
A container starts, dies and is restarted repeatedly. CrashLoopBackOff is the waiting state between attempts, not the cause.

## Steps
1. Confirm the cluster and namespace with `kubectl config current-context` before running anything else.
2. Run `kubectl describe pod <pod> -n <ns>`. Note which container fails (including init containers and sidecars), its Last State reason and exit code, and the events.
3. Read the dead instance: `kubectl logs <pod> -c <container> --previous`.
4. Interpret the code. Reason OOMKilled means the memory limit was hit. 137 without that reason is a SIGKILL from something else, often a failed liveness probe after the grace period. 139 is a segfault, 126 not executable, 127 command not found, 1 an application error. Exit 0 means the process finished, so a long-running workload is running the wrong command.
5. If probes appear in events, compare startup time with `initialDelaySeconds`, `periodSeconds` and `failureThreshold`. Slow starters need a startup probe.
6. Check command, args, env references, mounted ConfigMaps and Secrets, file permissions under the security context, and architecture of the image.
7. If it dies too fast to inspect, use `kubectl debug` to make a copy of the pod with a different command, rather than editing the live workload.
8. Fix in the source manifest, apply, and watch restarts for longer than the old crash interval.

## Watch out for
- Raising the memory limit without looking at usage over time just delays a leak.
- A liveness probe that checks a database turns one outage into a restart storm.
- Hand edits on the cluster get overwritten by GitOps or the next deploy.
- Printing env or Secret values into chat or tickets exposes them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The cause is stated with the evidence line that proves it, and the restart count stays unchanged over several former crash cycles.
