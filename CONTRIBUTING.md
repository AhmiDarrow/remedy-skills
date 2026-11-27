# Contributing skills

1. Fork / branch `feat/<skill-name>-v<version>`.
2. Add `skills/<name>/SKILL.md` (+ scripts if needed).
3. Open a PR — validation workflow must pass.
4. Maintainers review security; release updates the signed catalog.

Required frontmatter: `name`, `description`, `version` (prefer SemVer).

In `tools:` and in the playbook, name only tools the Remedy 2.0 runtime has (`read`,
`write`, `edit`, `bash`, `grep`, `glob`, `web.search`, `web.fetch`, and so on).

## License

Contributions are accepted under the same **[Apache License 2.0](./LICENSE)** as this repository and the main [RemedyAI](https://github.com/AhmiDarrow/RemedyAI) product (unless you and maintainers agree otherwise in writing). Prefer `license: Apache-2.0` in skill frontmatter to match that license.
