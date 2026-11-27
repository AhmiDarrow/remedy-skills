---
name: secret-scan-guidance
version: 1.0.1
description: >
  Scan a working tree and Git history for leaked credentials without echoing them, triage the hits and order the cleanup. Use when checking a repository for secrets or after one may have been committed.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - secrets
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - glob
metadata:
  source: library
  library_id: secret-scan-guidance
  official: true
  security_flags: []
---

# Secret Scan Guidance

## When to use
You need to find credentials in files you own or are authorised to inspect.

## Steps
1. Agree scope: working tree, all branches and tags, build outputs, CI configuration and logs.
2. Use an installed scanner with redaction on. For gitleaks, check the version's help (newer releases use `git` and `dir` subcommands, older ones `detect`) and pass `--redact`. Some scanners test found credentials against live services by default; disable verification unless the owner approves. Keep reports outside the repository and delete them when finished.
3. Without a scanner, search for private key headers, known token prefixes, connection strings with passwords, and assignments to names like secret, token or password. List filenames and line numbers only (`git grep -nIE` piped to keep the first two fields); do not print matching lines.
4. Cover history (the scanner's history mode, or the `git log --all` pickaxe listing only commits and filenames with `--oneline --name-only`, never `-p`), ignored files such as env files, notebooks and bundled assets.
5. Triage by type, location and context: real, test dummy, public by design, or unknown. Treat unknown as real. Report a type and location, never the value.
6. For a real secret: the owner revokes or rotates it first, because anything pushed may be copied already. Check its usage logs for misuse. Then remove it from the tree and load it from a secret store or environment.
7. Rewrite history only on request, with coordination: it changes commit IDs, and forks, clones and host caches may keep copies.
8. Add prevention: hook and CI scanning or host push protection, with narrow, commented allowlist entries.

## Watch out for
- Deleting the line in a new commit leaves the secret in history.
- Command output, tool transcripts and commit messages can leak what you found.
- Broad allowlists of whole test folders hide real keys.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The scanned scope and tool are stated, every hit is classified without revealing values, and each real secret has a rotation status and owner.
