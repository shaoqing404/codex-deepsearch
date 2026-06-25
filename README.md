# codex-deepsearch

A Codex-native skill that turns deep research into an evidence-led, reviewable workflow. It binds open-ended research to Codex's actual runtime — threads, workspaces, tools, `/goal` checkpoints, file edits, and optional delegated workers — so the output is decision-quality evidence that can survive review, not a long narrative or a link list.

Use it when a research answer may become a spec, roadmap, PRD, architecture decision, or implementation input, and when snippet-only or generated reasoning must not be sold as fact.

![License](https://img.shields.io/badge/license-Apache--2.0-blue)
![Skill version](https://img.shields.io/badge/version-0.1.0-green)
![Codex CLI](https://img.shields.io/badge/Codex%20CLI-native-blue)
![Agent Skills](https://img.shields.io/badge/Agent%20Skills-spec%20compliant-purple)
![Validation](https://img.shields.io/badge/quick__validate-passing-brightgreen)

---

## What it does

`codex-deepsearch` enforces a minimum contract on every research run:

1. **Frame** the decision question, audience, scope, exclusions, privacy boundaries, source priority, and stop conditions before searching.
2. **Scenario matrix** for cases where the answer differs by role, plan, platform, version, region, or execution path.
3. **Source ledger** and **claim ledger** filled before synthesis.
4. **Claim labels**: `retrieved_fact`, `source_summary`, `inference`, `needs_verification`, `conflict`.
5. **Evidence separation**: web/open/browser evidence, local file evidence, and user-provided evidence are kept distinct in both ledger and report.
6. **Tool-limit disclosure**: unavailable tools, paywalls, region blocks, and denied local access are recorded, never hidden.
7. **Review gate** runs before final output or before accepting any worker report.
8. **Readiness decision**: state whether the result can become spec, roadmap, product decision, or implementation input — and if not, name the blocking gaps.

Final status is one of `DONE`, `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, or `BLOCKED`. Uncertainty is always visible.

## When to use / not use

**Use when:**

- The user asks for evidence-backed research on current products, APIs, tools, laws, markets, models, or security advisories.
- Research may feed a spec, roadmap, PRD, architecture decision, or implementation plan.
- The user invokes `/goal` for a long-running research task that needs checkpoints and resumability.
- The user explicitly asks for `codex-with-cc-plus` or Claude Code worker delegation for parallel source scouting and skeptic review.
- Claims must be auditable — mapped to opened sources, with counter-evidence attempted.

**Do not use for:**

- Quick factual lookup where a single official page is enough.
- Pure code navigation (`rg`, `git grep`) when the user already knows the target files.
- Tasks that need implementation, not research — hand off to a spec/implementation skill after the review gate accepts.
- Exact-text search — use `Grep` directly.

## How it works

The skill follows the **Harness Engineering** discipline: the repository is the system of record, `AGENTS.md` is a map (not an encyclopedia), and detail lives in one-level-deep reference files loaded only when relevant.

```text
frame -> scenario matrix -> source discovery -> source ledger -> claim ledger
-> counter-evidence -> synthesis -> review gate -> handoff/readiness decision
```

- **Invariants over micromanagement.** The minimum contract above is enforced as a review gate; how the agent reaches each row in the ledger is left to the run.
- **Progressive disclosure.** `SKILL.md` is a short route map. Detailed rules live in `references/`. Reusable artifacts live in `templates/`.
- **Privacy-safe by default.** `workspace/`, `recordings/`, `transcripts/`, `tts/`, `audio/`, `.env`, secrets, and ignored files are off-limits unless the user explicitly authorizes them for the current task.
- **Optional delegation.** `codex-with-cc-plus` and Claude Code workers are optional layers. Main Codex always owns research design, ledgers, review, and final acceptance.

## Skill layout

```text
skills/codex-deepsearch/
├── SKILL.md                      # route map + minimum contract (Agent Skills spec)
├── agents/openai.yaml            # Codex UI metadata (display name, chip, default prompt)
├── references/                   # detailed rules, loaded on demand
│   ├── codex-runtime-model.md    # threads, workspaces, /goal, dirty worktree, tools
│   ├── research-workflow.md      # the 8-phase flow
│   ├── codex-tooling-rules.md    # web/search/browser/MCP/local evidence rules
│   ├── source-and-claim-ledgers.md
│   ├── review-gate.md
│   ├── privacy-and-repo-safety.md
│   └── delegation-with-codex-with-cc.md
└── templates/                    # durable artifacts the agent can fill
    ├── RESEARCH_DESIGN.md
    ├── SOURCE_LEDGER.md
    ├── CLAIM_LEDGER.md
    ├── DEEPSEARCH_REPORT.md
    └── REVIEW_GATE.md
```

Per Codex `skill-creator` conventions, the skill folder contains **no** `README.md`, `CHANGELOG.md`, or install guide — only files the agent uses. This repo-level `README.md` is the human-facing doc.

## Install

### OpenAI Codex CLI (primary target)

```bash
# from this repo, using Codex's bundled skill-installer helper
python /Users/mac/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo shaoqing404/codex-deepsearch --path skills/codex-deepsearch

# or manually
mkdir -p ~/.codex/skills
cp -r skills/codex-deepsearch ~/.codex/skills/
```

For local development, symlink instead of copy so edits take effect immediately:

```bash
ln -s "$PWD/skills/codex-deepsearch" ~/.codex/skills/codex-deepsearch
```

Codex auto-discovers skills in `~/.codex/skills/`. No restart is needed for edits to existing skills.

### TRAE (IDE / CLI / Work) — partial compatibility

The `SKILL.md` frontmatter (`name` + `description`) is Agent-Spec-compliant and will load in TRAE. Note, however, that the body references Codex-specific surfaces (`/goal`, `apply_patch`, `codex-with-cc-plus`); TRAE users should treat those as Codex-only and rely on the generic research-workflow and ledger sections.

```bash
# project skill (IDE/CLI/Work)
mkdir -p .trae/skills && cp -r skills/codex-deepsearch .trae/skills/

# global skill (IDE/Work)
cp -r skills/codex-deepsearch ~/.trae-cn/skills/

# or: TRAE Work → Skills marketplace → upload a .zip of skills/codex-deepsearch
```

### Claude Code — partial compatibility

```bash
# personal skill
mkdir -p ~/.claude/skills/codex-deepsearch
cp -r skills/codex-deepsearch/* ~/.claude/skills/codex-deepsearch/

# or project skill
mkdir -p .claude/skills/codex-deepsearch && cp -r skills/codex-deepsearch/* "$_"
```

Same caveat as TRAE: Codex-specific surfaces in the body do not apply. The ledgers, review gate, and privacy rules are tool-agnostic.

### ClawHub / OpenClaw (planned)

```bash
openclaw skills install codex-deepsearch
# or
npx clawhub@latest install shaoqing404/codex-deepsearch
```

Listing on ClawHub requires a signed manifest and moderated release — see the [Security](#security) section.

## Usage

Example prompts that should trigger the skill:

```text
Use $codex-deepsearch to determine whether Codex skills can be installed as
symlinked folders and whether that is suitable for local development.
```

```text
Use $codex-deepsearch to research whether this repo's planned feature should
become an implementation spec. Separate local code evidence from public docs.
```

```text
Use $codex-deepsearch. If codex-with-cc-plus is available, use delegated
researcher/reviewer workers to widen the search and run a skeptic review
before synthesis.
```

Expected output shape: a report with `Research Design`, `Scenario Matrix`, `Source Ledger`, `Claim Ledger`, `Counter-Evidence`, `Synthesis`, `Verification Gaps`, `Recommended Next Checks`, and `Review Gate` sections, ending with one of `DONE`, `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, or `BLOCKED`.

## Quality gate / Validation

Before publishing or after any edit, run:

```bash
# Codex skill-creator validator (mandated by AGENTS.md)
uv run --with pyyaml python \
  /Users/mac/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  skills/codex-deepsearch
```

Hard conventions enforced by all target tools:

- `name` matches the parent directory and is lowercase-hyphen, ≤64 chars.
- `description` is ≤1024 chars, third-person, with explicit "when to use" triggers.
- `SKILL.md` body stays under 500 lines; reference files are one level deep.
- No Codex-UI-only or Claude-Code-only frontmatter (`disable-model-invocation`, `context: fork`, `allowed-tools`) in the shared `SKILL.md` — they would break other tools.

Forward-test on a realistic prompt (not "review this skill") with a fresh subagent before trusting a revision.

## Security

- **No secrets in scripts or assets.** The skill ships no scripts in v1; templates are plain Markdown.
- **Privacy-first.** `references/privacy-and-repo-safety.md` forbids reading `workspace/`, `recordings/`, `transcripts/`, `tts/`, `audio/`, `.env`, secrets, ignored files, and obvious personal exports unless the user explicitly authorizes them for the current task.
- **No git mutation.** Never `git add .`, never commit, push, reset, or clean unless the user explicitly asks.
- **No external uploads.** Private local content is never pasted into web services, search engines, or external APIs.
- **ClawHub listing** (when published) will require a signed manifest and a moderated release scan.

## Compatibility matrix

| Agent            | Status | Install path                                 | Notes                                                       |
| ---------------- | ------ | -------------------------------------------- | ----------------------------------------------------------- |
| OpenAI Codex CLI | Native | `~/.codex/skills/codex-deepsearch/`          | Primary target; uses `/goal`, `apply_patch`, optional `agents/openai.yaml` |
| TRAE IDE         | Partial| `.trae/skills/` or `~/.trae-cn/skills/`     | Frontmatter loads; Codex-specific body sections ignored     |
| TRAE CLI         | Partial| `.traecli/skills/`                           | Reads IDE dirs too                                          |
| TRAE Work        | Partial| `.trae/skills/` or marketplace `.zip` upload | Same caveat as TRAE IDE                                     |
| Claude Code      | Partial| `~/.claude/skills/` or `.claude/skills/`     | Frontmatter loads; Codex-specific body sections ignored     |
| ClawHub          | Planned| `~/.openclaw/skills/`                        | Pending signed manifest + moderated release                 |

## Repository conventions

This repo follows the Harness Engineering discipline:

- **`AGENTS.md` is a map.** Roughly 30 lines: boundaries, layout, validation command. It points to `docs/` and `specs/` for depth.
- **`docs/` is the system of record.** `architecture.md`, `roadmap.md`, and `index.md` hold design decisions; `specs/` holds implementation and forward-test plans.
- **Plans are first-class artifacts.** `specs/001-codex-deepsearch-skill.md` is the v1 spec; `specs/002-forward-test-plan.md` defines acceptance and failure signals.
- **Doc gardening.** When a reference file no longer reflects real behavior, update it in the same PR as the skill change. Do not leave stale rules.

## Roadmap

See [docs/roadmap.md](docs/roadmap.md). Summary:

- **v1** — local skill, instruction-first, template-backed. ✅
- **v1.1** — forward-test on real research tasks; tighten trigger wording if implicit invocation is too broad or too narrow.
- **v2** — package as a Codex plugin if distribution requires managed install, hooks, or multiple related skills.

## License

Apache-2.0.
