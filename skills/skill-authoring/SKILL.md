---
name: skill-authoring
version: 1.0.0
description: >
  Write or improve an assistant skill whose description triggers correctly and whose body teaches non-obvious steps and checks. Use when creating a SKILL.md or fixing a skill that is ignored or misfires.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - skills
  - prompting
kind: native
status: discovered
tools:
  - skill.search
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: skill-authoring
  official: true
  domain: llm
  security_flags: []
---

# Skill Authoring

## When to use
A recurring task should become a reusable playbook, or an existing one is not helping.

## Steps
1. Search existing skills first and extend one rather than creating an overlapping copy.
2. Gather evidence: real requests, and where an assistant without the skill went wrong. If it already does well, a skill is not needed.
3. Read the target loader's format rules and a working neighbouring skill for front matter and layout.
4. Write the description as the routing signal: what it does, when to use it, in words users would say. Distinguish it from close neighbours.
5. Write the body for the mistakes observed: order of work, exact commands that were verified, decision rules, failure modes and where to stop for approval.
6. Cut general advice the assistant already follows. Give reasons where judgement is needed.
7. Move long references and fragile mechanical steps into supporting files or scripts if the format supports them, and say when to load each.
8. List only the tools the task needs.
9. Test triggering with requests that should match, near misses that should not, and indirect phrasings.
10. Run realistic tasks with and without the skill, compare results, and revise from the traces.

## Watch out for
- Examples copied from one project can make the skill apply that project's paths everywhere.
- A description stuffed with keywords steals requests from other skills.
- Secrets, private data or text copied from sources without permission do not belong in a skill.
- Retest triggering after neighbours change.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The format check passes, trigger tests route correctly, and at least one realistic task shows a concrete improvement over the no-skill run.
