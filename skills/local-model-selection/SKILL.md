---
name: local-model-selection
version: 1.0.0
description: >
  Pick a local language model and quantization that fit the hardware, licence and task, and prove it on real examples. Use when someone wants to run a model on their own machine.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - local-models
  - hardware
kind: native
status: discovered
tools:
  - bash
  - web.search
  - web.fetch
  - read
  - write
metadata:
  source: library
  library_id: local-model-selection
  official: true
  domain: llm
  security_flags: []
---

# Local Model Selection

## When to use
Choosing which open-weight model to run locally, or replacing one that is too slow or weak.

## Steps
1. Read the real hardware: RAM, each GPU and its VRAM (`nvidia-smi` for NVIDIA; use the platform's tool otherwise), free disk, OS.
2. Define the task, languages, context length needed, acceptable first-token delay and speed, concurrency, and whether tool calls or structured output are required.
3. Check current candidates on official model pages with `web.search`; this field changes faster than memory. Read each licence for the intended use.
4. Estimate memory: weights are roughly parameter count times bits per weight divided by 8, plus context cache that grows with context length and parallel requests, plus runtime overhead. Use the actual file size when known.
5. Choose quantization: start at a mid level such as 4-bit if memory requires, and compare with a higher one. Very low bit widths tend to lose noticeably more quality.
6. Prefer fitting fully on the GPU; spilling layers to CPU usually slows generation sharply.
7. Confirm the runtime supports the format and architecture and has the right chat template.
8. State download size and source, get approval, and fetch from the publisher or a source the user trusts, preferring weight-only formats such as safetensors or GGUF.
9. Run 20 or more real task examples on two or three candidates with the same settings.
10. Record quality, peak memory, prompt processing speed, generation speed and context used.

## Watch out for
- An advertised maximum context does not mean it fits in memory or performs well.
- Public leaderboard rank may not predict the user's task.
- Repository code that must run to load a model needs the user's review and consent.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chosen model runs on this machine at the required context and passes the user's examples, with measurements and licence recorded.
