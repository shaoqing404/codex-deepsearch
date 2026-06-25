# Codex DeepSearch Architecture

`codex-deepsearch` is a Codex-native execution and review layer for deep research. It does not replace generic research method skills; it binds evidence-led research to Codex's runtime, tools, workspace rules, validation habits, and optional worker orchestration.

## Layers

| Layer | Responsibility |
|---|---|
| generic DeepSearch | Research design, scenario matrix, ledgers, counter-evidence, synthesis |
| codex-deepsearch | Codex tool use, local/web evidence separation, repo safety, `/goal` checkpoints, review gate, readiness decision |
| codex-with-cc-plus | Optional delegated worker layer for wider search, parallel analysis, and independent review |
| project-specific skills | Domain constraints, private data contracts, templates, and repo-specific workflows |

## Fact Source

The plugin source lives at:

```text
/Users/mac/Developer/element_workspace/codex-deepsearch/plugins/codex-deepsearch
```

The skill inside the plugin lives at:

```text
/Users/mac/Developer/element_workspace/codex-deepsearch/plugins/codex-deepsearch/skills/codex-deepsearch
```

The Codex plugin marketplace catalog lives at:

```text
/Users/mac/Developer/element_workspace/codex-deepsearch/.agents/plugins/marketplace.json
```

For direct skill install (without the plugin wrapper), the local Codex installation should point to the inner skill folder:

```text
/Users/mac/.codex/skills/codex-deepsearch
```

Using a symlink keeps development and installed skill behavior aligned.

## Design Choices

- Keep `SKILL.md` short and procedural.
- Put detailed rules in one-level references.
- Use Markdown templates instead of scripts for v1.
- Make `codex-with-cc-plus` optional and task-file-driven.
- Treat `/goal` as a checkpointed long-task control surface.
- Require review before final synthesis becomes implementation input.
- Ship as a Codex plugin (`.codex-plugin/plugin.json` + marketplace catalog) so users can install via `codex plugin marketplace add shaoqing404/codex-deepsearch`, while keeping the inner skill Agent-Spec-compliant for Trae and Claude Code direct install.
