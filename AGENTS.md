# AGENTS.md

This repository develops the local Codex skill `codex-deepsearch`.

## Boundaries

- Do not modify `/Users/mac/Developer/DeepMatch` from this repo.
- Keep the reusable skill project-agnostic.
- Do not read private or ignored materials from unrelated repositories.
- Do not install system tools.
- Do not modify system Python; use `uv` for Python validation.
- Do not commit, push, or publish unless explicitly asked.

## Layout

- `plugins/codex-deepsearch/`: installable plugin source. The skill lives at `plugins/codex-deepsearch/skills/codex-deepsearch/`.
- `.agents/plugins/marketplace.json`: Codex plugin marketplace catalog for `codex plugin marketplace add shaoqing404/codex-deepsearch`.
- `specs/`: implementation and forward-test plans.
- `docs/`: architecture and roadmap notes.

## Validation

Run skill validation after changing the skill:

```bash
uv run --with pyyaml python /Users/mac/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/mac/.codex/skills/codex-deepsearch
uv run --with pyyaml python /Users/mac/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/mac/.agents/skills/codex-deepsearch
```

If the install path is not linked yet, validate the source path:

```bash
uv run --with pyyaml python /Users/mac/.codex/skills/.system/skill-creator/scripts/quick_validate.py /Users/mac/Developer/element_workspace/codex-deepsearch/plugins/codex-deepsearch/skills/codex-deepsearch
```
