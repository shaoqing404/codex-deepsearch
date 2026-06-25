# Roadmap

## v1: Local Skill

- Create the skill source tree.
- Install through `~/.codex/skills/codex-deepsearch`.
- Validate with skill-creator quick validation.
- Keep the skill instruction-first and template-backed.

## v1.1: Usage Hardening

- Forward-test on real research tasks.
- Tighten trigger wording if implicit invocation is too broad or too narrow.
- Add ledger lint script only if manual ledgers drift repeatedly.

## v2: Plugin Packaging

- Package as a Codex plugin if distribution requires managed install, hooks, or multiple related skills.
- Consider optional MCP/tool dependency declarations only when the dependency is real and stable.
