# Spec 001: Codex DeepSearch Skill

## Summary

Create a reusable local Codex skill that turns deep research into a Codex-native, auditable workflow with source/claim ledgers, tool-limit disclosure, privacy-safe local inspection, `/goal` checkpoints, review gates, and optional `codex-with-cc-plus` delegation.

## Goals

- Improve depth of Codex research reports by forcing evidence ledgers before synthesis.
- Make local file evidence, web evidence, connector evidence, snippets, and worker reports visibly distinct.
- Prevent snippet-only or generated reasoning from becoming high-confidence facts.
- Support long-running `/goal` DeepSearch through checkpoints and completion gates.
- Allow users with `codex-with-cc-plus` to delegate source discovery and analysis while preserving main-thread acceptance.
- Keep project-specific DeepSearch concerns out of the generic Codex skill.

## Non-Goals

- Do not depend on DeepMatch.
- Do not require Claude Code or `codex-with-cc-plus`.
- Do not install system tools.
- Do not add backend services, databases, or web apps.
- Do not automate git commits.

## User Stories

- As a Codex user, I can ask for deep research and receive a report whose claims map to opened sources.
- As a Codex user, I can see which claims are retrieved facts, source summaries, inferences, conflicts, or still unverified.
- As a Codex user, I can run a long `/goal` research task and resume from explicit checkpoints.
- As a Codex user with `codex-with-cc-plus`, I can delegate source scouting and skeptic review while preserving main-thread acceptance.
- As a user with private local data, I can trust the skill to avoid ignored/private material unless explicitly authorized.

## Requirements

- The skill must include valid `SKILL.md` frontmatter with `name` and `description`.
- The skill must include references for runtime model, workflow, ledgers, tooling rules, optional delegation, review gate, and privacy safety.
- The skill must include templates for research design, source ledger, claim ledger, report, and review gate.
- The installed skill must validate with `skill-creator` quick validation.
- The development repo must stay outside `/Users/mac/Developer/DeepMatch`.

## Acceptance Criteria

- `quick_validate.py` passes for the installed skill.
- `SKILL.md` explicitly states the 8-item minimum contract.
- Review gate includes spec, roadmap, and implementation readiness checks.
- Delegation reference treats `codex-with-cc-plus` as optional.
- Privacy reference forbids private/ignored materials by default.
- No DeepMatch files are modified.

## Open Follow-Ups

- Forward-test on a real Codex research prompt.
- Consider adding deterministic ledger linting if repeated usage shows format drift.
- Consider packaging as a plugin if distribution beyond this machine becomes important.
