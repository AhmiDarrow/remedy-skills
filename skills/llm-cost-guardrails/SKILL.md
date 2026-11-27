---
name: llm-cost-guardrails
version: 1.0.1
description: >
  Measure and cap the token cost and latency of model-powered features with per-request limits, budgets and tested savings. Use when model bills or response times are high or unbounded.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - cost
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: llm-cost-guardrails
  official: true
  security_flags: []
---

# Llm Cost Guardrails

## When to use
An application calls a language model and spend or latency needs to be known and bounded.

## Steps
1. Find every call site, including retries, agent loops, background jobs and embedding calls.
2. Record per call: feature, model, input, cached and output tokens from the provider's usage data, latency, retries, outcome and a tenant id where relevant. Do not log prompt text by default.
3. Calculate cost with current prices from the provider's price list, kept in configuration with a date. Report cost per successful task as well as per call.
4. Rank features by total cost and inspect real request sizes. Look for repeated history, oversized tool results, unused tool definitions and excess retrieved passages.
5. Set hard limits: input size, maximum output tokens, loop steps, tool calls, wall time and retries per task. Detect truncated output through the stop reason and handle it explicitly.
6. Add budgets per user or tenant and a global ceiling, checked before the call with allowance for concurrent requests. Define the behaviour at the limit: queue, degrade or refuse with a clear message. Add alerts and a kill switch.
7. Apply savings one at a time: trim context; use prompt caching with stable content first, then verify cache hits in usage data; batch work that can wait if the provider offers it; route easy requests to a cheaper model.
8. Evaluate each change on a fixed set of real cases for quality, cost and latency before rollout. Agree a spend limit before paid evaluation runs. Include the cost of failures that fall back to a stronger model.
9. Test that a runaway loop and a burst of requests stop at the limits, using a stubbed model client or test limits set very low, not an unbounded run against the paid API.

## Watch out for
- A timestamp or user id early in the prompt defeating prefix caching.
- Response caches keyed without user permissions, model or prompt version, leaking or serving stale answers.
- Truncating history from the wrong end and dropping instructions or tool call and result pairs.
- Streaming calls cancelled on the client while the server keeps generating.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Spend is visible per feature, limits are proven by tests, and each savings change has before and after quality and cost figures.
