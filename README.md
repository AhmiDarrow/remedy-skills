# Remedy Skills

**Extra playbooks for your local AI partner — install only what you need.**

This is the public **Skills Library** for [Remedy](https://github.com/AhmiDarrow/RemedyAI).
Skills are portable instruction packs the agent can load on demand — same idea as
the ones that ship with the app, except **you** pick what lands on your machine.
Nothing here runs, and nothing runs scripts, until you **Trust** it.

```text
You  →  Skills → Library  →  Install (quarantine)  →  Trust  →  ready to use
```

- **[Latest catalog release](https://github.com/AhmiDarrow/remedy-skills/releases/latest)** — signed `catalog.json` + skill packs  
- **[Full skill index](./SKILLS.md)** — every pack, grouped and alphabetical (kept current automatically)

---

## Continuity, not clutter

Remedy already ships a small set of **bundled** skills for everyday partner work.
This repo is the wider shelf: engineering, gaming, design, content, ops, and
personal workflows — written as real procedures, not empty titles.

The library stays **local-first**, same as Remedy itself:

- **You choose** what to install — nothing bulk-dumps into the agent  
- **Quarantine first** — packs land inert; scripts stay blocked until Trust  
- **Signed catalog** — downloads limited to this project’s GitHub releases  
- **Installs live on your PC** under `~/.remedy/skills/`

Each skill says when to use it, the steps, tool hints, and what “done” looks like.

---

<!-- BEGIN AUTO-SKILLS-LIST -->

## What’s in the library (830 skills)

Snapshot of packs on this branch as of 2026-11-27. Descriptions and the full alphabetical list live in **[SKILLS.md](./SKILLS.md)**.

| Area | # | A few examples |
|------|--:|----------------|
| Backend & APIs | 69 | `aggregate-invariant-design`, `api-client-sdk`, `api-contract-review`, `api-deprecation-sunset` · +65 more |
| Content & writing | 74 | `app-listing-copy`, `audio-loudness-normalize`, `audio-transcription-local`, `author-voice-match` · +70 more |
| Data | 57 | `ab-test-readout`, `ab-test-sample-size`, `anomaly-detection-thresholds`, `bookkeeping-month-close` · +53 more |
| Design & UX | 31 | `cli-ux-polish`, `color-system`, `deceptive-pattern-audit`, `design-brief` · +27 more |
| Docs & process | 65 | `adr-write`, `agent-repo-instructions`, `behavior-spec-from-code`, `breaking-news-verification` · +61 more |
| Frontend | 80 | `a11y-design-review`, `accessible-combobox`, `accessible-drag-drop`, `anchored-popover-positioning` · +76 more |
| Gaming | 44 | `boss-fight-design`, `combat-feel-tuning`, `game-accessibility`, `game-ai-behavior` · +40 more |
| Git & release | 26 | `batch-pr-integration`, `branch-hygiene`, `change-hotspot-analysis`, `cherry-pick-commit` · +22 more |
| LLM & agents | 21 | `agent-context-management`, `agent-loop-design`, `cloud-cost-spike-investigation`, `embedding-model-migration` · +17 more |
| Ops & reliability | 72 | `alert-noise-reduction`, `app-store-submission-prep`, `artifact-promotion-pipeline`, `backup-restore-drill` · +68 more |
| Other | 2 | `hello-library`, `license-compliance` |
| Personal assistant | 117 | `account-recovery-readiness`, `after-death-admin-list`, `allergen-aware-guest-menu`, `appliance-repair-triage` · +113 more |
| Security | 58 | `audit-log-design`, `auth-session-review`, `backup-strategy-design`, `bash-script-hardening` · +54 more |
| Testing | 38 | `acceptance-criteria`, `benchmark-micro`, `browser-automation-safe`, `browser-download-retrieval` · +34 more |
| Tooling & languages | 76 | `algorithmic-complexity`, `battery-sleep-current-reduction`, `bug-intake-triage`, `cmake-modern-target-refactor` · +72 more |

**830 total** — skim the [full list](./SKILLS.md), or open **Skills → Library** in Remedy Desktop and install only what you need.

<!-- END AUTO-SKILLS-LIST -->

---

## Try it

About a minute if you already have Remedy Desktop. If not, install Remedy 2.0 (a
Go runtime with desktop and phone apps written in Rust) from the installers on the
[RemedyAI releases page](https://github.com/AhmiDarrow/RemedyAI/releases/latest):

1. Open **Skills** → **Library**
2. Search or browse, then **Install** (lands in quarantine)
3. Skim the pack — when you’re happy, **Trust**
4. Ask Remedy to use that workflow in chat

Prefer reading first? Start with the [full list](./SKILLS.md) or open any
`skills/<name>/SKILL.md`.

---

## What’s in a skill

A skill is a folder with a `SKILL.md` (short YAML frontmatter + the playbook),
and sometimes a helper script. The agent sees the short description first, then
loads the full body when the task matches — so you don’t pay for a wall of
instructions on every turn.

Packs here are meant to be **usable**: concrete steps, tool hints, and safety
notes (no secrets; confirm before anything destructive). Tool hints use Remedy 2.0
tool names, such as `read`, `write`, `edit`, `bash`, `grep`, `web.search` and
`web.fetch`.

---

## Security — you hold Trust

Same posture as importing a ZIP in Remedy: power for the owner, not a free pass
for random packs.

| Layer | What we ship |
|-------|----------------|
| **Signed catalog** | Ed25519 signature checked before the client trusts the list |
| **Release assets only** | Installs come from this repo’s GitHub releases (no random hosts) |
| **Checksums** | SHA-256 of each zip required |
| **Quarantine by default** | Scripts blocked until you **Trust** in Remedy |
| **Zip safety** | Zip-slip protected extraction |

Details: [SECURITY.md](./SECURITY.md).

---

## Contribute

Ideas and PRs welcome when they stay practical and safe.

1. Read [CONTRIBUTING.md](./CONTRIBUTING.md)
2. Add `skills/<name>/SKILL.md` (scripts only when they actually help)
3. Open a PR — validation CI should pass

Please don’t ship secrets, or instructions that hinge on another product’s brand
as the only path — keep guidance portable so anyone can follow it.

---

## Maintainers

After you add or edit skills:

```bash
python scripts/generate_skills_list.py   # SKILLS.md + README library section
python scripts/build_catalog.py          # catalog.json (also refreshes the list)

# Public release catalog (download URLs → this repo’s release assets):
python scripts/build_catalog.py --github-urls --release-tag v2.0.0
export REMEDY_SKILLS_SIGNING_KEY="..."   # base64 Ed25519 seed
python scripts/sign_catalog.py
```

CI keeps the docs honest:

| Workflow | Role |
|----------|------|
| **update-skills-list** | On skill changes → refresh `SKILLS.md` + README section |
| **validate-skill-submission** | PR checks for new packs |
| **catalog-sync** | On release → rebuild catalog, list, and signature |

---

## License

**Same as [RemedyAI](https://github.com/AhmiDarrow/RemedyAI):** the
[Apache License 2.0](./LICENSE) (copyright Ahmi Darrow; see [NOTICE](./NOTICE)).

Skill packs and catalog scripts in this repo are covered by that LICENSE unless
a pack’s frontmatter names a different license. Remedy the product is documented
in the [main repo](https://github.com/AhmiDarrow/RemedyAI).

---

*Part of the Remedy local partner stack — continuity on your PC, library on your terms.*

---

## Support

If this library helps you, you can support development on Patreon:

**[patreon.com/cw/AhmiDarrow](https://www.patreon.com/cw/AhmiDarrow)**
