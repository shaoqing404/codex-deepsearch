# Documentation Index

This index is the map. Depth lives in the linked files. The `AGENTS.md` at the repo root is the entry point for agents; this file is the entry point for humans.

## Start here

| File | Purpose |
|---|---|
| [../README.md](../README.md) | Project overview, install, usage, compatibility matrix |
| [../AGENTS.md](../AGENTS.md) | Agent-facing map: boundaries, layout, validation command |
| [architecture.md](architecture.md) | Skill layers, source of truth, design choices |
| [roadmap.md](roadmap.md) | Staged hardening plan (v1 → v1.1 → v2) |

## Specifications

| File | Purpose |
|---|---|
| [../specs/001-codex-deepsearch-skill.md](../specs/001-codex-deepsearch-skill.md) | v1 skill specification: goals, non-goals, acceptance criteria |
| [../specs/002-forward-test-plan.md](../specs/002-forward-test-plan.md) | Forward-test prompts and acceptance/failure signals |

## Plugin and skill source

| File | Purpose |
|---|---|
| [../.agents/plugins/marketplace.json](../.agents/plugins/marketplace.json) | Codex plugin marketplace catalog |
| [../plugins/codex-deepsearch/.codex-plugin/plugin.json](../plugins/codex-deepsearch/.codex-plugin/plugin.json) | Plugin manifest (name, version, skills pointer, install-surface metadata) |
| [../plugins/codex-deepsearch/skills/codex-deepsearch/SKILL.md](../plugins/codex-deepsearch/skills/codex-deepsearch/SKILL.md) | Trigger, minimum contract, routing |
| [../plugins/codex-deepsearch/skills/codex-deepsearch/references/](../plugins/codex-deepsearch/skills/codex-deepsearch/references/) | Detailed operating rules (runtime, workflow, ledgers, tooling, review, privacy, delegation) |
| [../plugins/codex-deepsearch/skills/codex-deepsearch/templates/](../plugins/codex-deepsearch/skills/codex-deepsearch/templates/) | Reusable report and ledger templates |
| [../plugins/codex-deepsearch/skills/codex-deepsearch/agents/openai.yaml](../plugins/codex-deepsearch/skills/codex-deepsearch/agents/openai.yaml) | Codex UI metadata (display name, chip, default prompt) |

## Reading order for a new contributor

1. [../AGENTS.md](../AGENTS.md) — what this repo is and is not.
2. [architecture.md](architecture.md) — why the skill is layered this way.
3. [../plugins/codex-deepsearch/skills/codex-deepsearch/SKILL.md](../plugins/codex-deepsearch/skills/codex-deepsearch/SKILL.md) — the route map the agent sees.
4. [../specs/001-codex-deepsearch-skill.md](../specs/001-codex-deepsearch-skill.md) — what v1 must satisfy.
5. [../specs/002-forward-test-plan.md](../specs/002-forward-test-plan.md) — how v1 is forward-tested.

## Doc gardening

When a file no longer reflects real behavior, update it in the same change as the skill edit. Stale rules are worse than missing rules — agents cannot tell which still hold.
