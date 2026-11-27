---
name: repo-public-readiness
version: 1.0.0
description: >
  Prepare a private repository to be made public by checking history, secrets, personal data, licences and docs. Use before open-sourcing a project or changing a repository's visibility.
author: Remedy Official
license: Apache-2.0
tags:
  - git
  - repo-hygiene
  - open-source
kind: native
status: discovered
tools:
  - bash
  - grep
  - glob
  - read
  - edit
  - write
metadata:
  source: library
  library_id: repo-public-readiness
  official: true
  domain: git
  security_flags: []
---

# Repo Public Readiness

## When to use
Publication exposes every commit, branch, tag and often more than the files visible today, and cannot be reliably taken back.
## Steps
1. Make a list of what becomes visible: all refs, full history, issues, pull requests, releases, wiki, CI logs and attached artifacts.
2. Scan all history, not only the working tree, with a secret scanner such as gitleaks, using its redaction option (`--redact`) so values are not printed or saved in reports. Any real secret ever committed must be rotated.
3. Search files and history for personal and internal data: names, emails, home directory paths, internal hosts, customer samples. Check commit author and committer fields with `git log --all --format="%an <%ae> / %cn <%ce>"` deduplicated, and look inside images, fixtures and logs including metadata.
4. Check rights: your authority to publish, third-party code and assets with their licences and required notices.
5. Ask the user to choose a licence; without one others have no general permission to reuse the code.
6. Decide history: keep it, or start a fresh repository from a cleaned tree. Fresh is safer when findings are widespread; keep the private original.
7. Make a clean clone work from the readme alone, with example config in place of real values.
8. Review CI for self-hosted runners and workflows that expose secrets to outside contributions.
9. Present findings and let the user flip visibility.
## Watch out for
- Cleaning only the default branch.
- Believing a deleted file is gone.
- Debug scripts and notes containing candid remarks or private plans.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
History and hosted content have been scanned, findings are resolved or accepted by the user, a licence is chosen and a clean clone builds.
