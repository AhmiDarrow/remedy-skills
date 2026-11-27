---
name: cloud-cost-spike-investigation
version: 1.0.0
description: >
  Explain a sudden rise in a cloud bill by narrowing it to service, usage type, resource and the change that started it. Use when spend jumps or a budget alert fires.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - cloud
  - cost
kind: native
status: discovered
tools:
  - bash
  - read
  - web.fetch
  - owner.notify
metadata:
  source: library
  library_id: cloud-cost-spike-investigation
  official: true
  domain: ops
  security_flags: []
---

# Cloud Cost Spike Investigation

## When to use
Spend is unexpectedly higher. This is investigation of infrastructure usage, not financial advice.

## Steps
1. Pin the start: daily cost over at least 60 days, grouped by service. Allow for billing data lagging by a day or more and for monthly charges posting on one date.
2. In the service that moved, group by usage type, then region, account and resource or tag.
3. Separate more usage from a changed price: expired commitment or credit, ended free tier, new support charge or tax.
4. Check frequent hidden drivers: data transfer between zones or regions, NAT processing, log and metric ingestion, request counts on object storage, orphaned disks, snapshots and public IPs.
5. Correlate the start with deploys, infrastructure changes and audit log events.
6. If you find compute in unused regions or resources nobody created, treat it as credential compromise and switch to containment immediately.
7. Estimate the daily burn of the cause and tell the owner.
8. Propose the smallest fix, its side effects and whether it is reversible. Get approval before stopping or deleting anything.
9. Add a budget or anomaly alert that would have caught it sooner.

## Watch out for
- Stopped instances still bill for attached storage and often for reserved addresses.
- Deleting snapshots or logs to save money can break recovery or retention duties.
- Cost explorer APIs themselves may charge per request; check before looping.
- Blended or amortised views move commitment charges around and can invent or hide a spike.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The increase is attributed to named resources and a cause with figures, and daily cost data after the fix shows the expected drop or the remaining gap is stated.
