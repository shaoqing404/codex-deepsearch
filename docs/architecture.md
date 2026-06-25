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

The skill source lives at:

```text
/Users/mac/Developer/element_workspace/codex-deepsearch/skills/codex-deepsearch
```

The local Codex installation should point to that folder:

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
