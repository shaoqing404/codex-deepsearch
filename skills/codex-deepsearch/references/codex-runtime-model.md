# Codex Runtime Model

Use this reference when DeepSearch depends on Codex-specific behavior rather than generic research technique.

## Runtime Surfaces

Codex work happens inside a thread attached to a workspace. A turn may include user messages, commentary progress updates, tool calls, file reads, file edits, validation commands, and a final answer. Treat the final answer as a handoff backed by observed evidence, not as the evidence itself.

Codex skills use progressive disclosure:

- Metadata: `name`, `description`, and path are initially visible.
- `SKILL.md`: loaded when Codex selects the skill.
- `references/`, `templates/`, `scripts/`, and `assets/`: read or used only when relevant.

For DeepSearch, keep `SKILL.md` as the route map. Put detailed rules in references.

## Workspace And Files

Local files are evidence only when actually read or otherwise inspected. Record the retrieval method in the source ledger.

Before inspecting local files:

- Identify the current workspace and repository root.
- Read relevant `AGENTS.md` or repo docs when they govern the task.
- Check for private or ignored directories before broad search.
- Use `rg --files` or targeted `rg` before opening many files.

Before writing:

- Confirm the user asked for durable artifacts or implementation.
- Check `git status --short`.
- Prefer writing to an explicitly authorized research output directory.
- Use `apply_patch` for manual edits.

## Dirty Worktree

A dirty worktree means the user or another process may have work in progress. Do not revert, overwrite, stage, or commit unrelated changes.

When research requires edits:

- State the target files before editing.
- Keep changes narrow.
- Re-check `git diff` for touched files.
- Do not use destructive git commands.

## Tools

Codex tool outputs are observations with limits:

- `web.search_query`: discovery and snippets; snippets are not retrieved facts.
- `web.open`: opened web page evidence, subject to page access and quote limits.
- Browser/Chrome tools: visual or interactive page evidence; record screenshots or observations as such.
- Shell reads: local file evidence; record path and access date.
- MCP/app connectors: connector evidence; record connector/tool and whether content is private/user-authorized.
- `apply_patch`: mutation, not evidence by itself.

## Commentary And Final

Use commentary updates to say what context is being gathered, what phase is active, and what blockers appeared. Keep them concise.

Use the final response to report:

- Answer or handoff.
- Evidence basis and key uncertainty.
- Review gate status.
- Whether the result can become spec, roadmap, product decision, or implementation input.

## Goal Mode

`/goal` is a persistent objective, not permission to drift. For long DeepSearch, use `/plan` to shape scope and `/goal` to maintain execution state.

In goal mode, maintain checkpoints:

- Decision question and audience.
- Current phase.
- Accepted source and claim counts.
- Open verification gaps.
- Next checks.
- Review gate status.
- Stop condition.

After resume or interruption, re-establish workspace, privacy boundaries, dirty worktree state, tool availability, and current phase before continuing.

Do not mark a goal complete merely because a report exists. Completion requires the review gate to accept the evidence, or the final handoff must clearly state `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, or `BLOCKED`.
