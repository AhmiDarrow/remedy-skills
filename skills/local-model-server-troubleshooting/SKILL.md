---
name: local-model-server-troubleshooting
version: 1.0.0
description: >
  Fix a self-hosted model server that is slow, out of memory, truncating context or producing garbled replies. Use when local inference misbehaves through its API or app.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - local-models
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - jobs
metadata:
  source: library
  library_id: local-model-server-troubleshooting
  official: true
  domain: llm
  security_flags: []
---

# Local Model Server Troubleshooting

## When to use
A locally served model loads badly, answers strangely, forgets earlier text or runs far below expected speed.

## Steps
1. Record runtime name and version, model file, quantization, launch settings and the exact failing request.
2. Read startup logs: backend detected, layers offloaded to GPU, context size, memory allocated. A GPU build can silently fall back to CPU.
3. Check effective context size. Server defaults may be far below the model maximum, and overflow may truncate the start, including the system prompt. Compare token counts.
4. For garbled output, endless generation or role text in replies, verify the chat template, stop tokens and whether a base model is being used as a chat model. Compare raw rendered prompt with the model card.
5. Retry with a short prompt, no custom sampling and temperature 0.
6. For out-of-memory, reduce context, parallel slots or batch size, then use a smaller quantization or fewer GPU layers. Change one at a time.
7. For speed, measure model load, prompt processing and generation separately. Check memory use by other processes, thermal limits and whether the model reloads between requests.
8. For tool calls or JSON failures, confirm that this runtime and template support the feature on the installed version.
9. If output remains wrong, verify the file checksum and try a known-good small model.
10. Check the listen address. Keep it on localhost unless network access is intended and authenticated.

## Watch out for
- An API that imitates a hosted service may silently ignore parameters it does not support.
- Stop only the server process you identified, not every process with a matching name.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failing request succeeds repeatably, logs show the intended device and context size, and the changed setting is documented.
