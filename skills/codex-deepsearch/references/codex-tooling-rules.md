# Codex Tooling Rules

Use these rules to keep Codex DeepSearch honest about how evidence was obtained.

## Web And Search

Use web/search when:

- The user explicitly asks to search, verify, or find current information.
- The topic is temporally unstable: APIs, docs, pricing, laws, product features, models, market facts, schedules, security advisories, or company/person status.
- Recommendations could affect material time, money, legal, medical, financial, security, or product decisions.
- The answer needs direct quotes, links, citations, or precise source attribution.

Search result snippets are `source_summary`, not `retrieved_fact`. Open official or primary pages when possible.

Record:

- Query.
- Search tool used.
- Pages opened.
- Access date.
- Tool limitations.

## Official Source Priority

Prefer:

1. Official docs, specs, standards, law, changelogs, release notes, source repositories, filings, or papers.
2. Maintainer issues, RFCs, engineering notes, and implementation docs.
3. High-quality third-party analysis.
4. Community forums and blogs for operational clues only.

Use third-party sources for context, not as the sole basis for high-confidence product/API claims.

## Local Files

Use local file inspection when:

- The user asks about a repo, local implementation, local docs, or existing artifacts.
- A claim depends on actual code/config rather than public docs.
- You need to verify whether a proposed plan fits the codebase.

Prefer:

- `rg --files`
- targeted `rg`
- `sed -n`
- `git status --short`
- `git diff -- <path>`

Do not read private or ignored material unless authorized.

## Tool Limit Recording

Always record relevant limits:

- Web search disabled.
- Web open/fetch unavailable.
- Browser or Chrome unavailable.
- MiniMax MCP web_search unavailable.
- OpenAI docs MCP unavailable.
- Login/paywall/bot/region block.
- Local file permission denied.
- User denied private-data access.
- Worker unavailable or refused.

Tool limitations affect status. A useful but limited report is usually `DONE_WITH_CONCERNS`, not `DONE`.

## Browser Evidence

Browser screenshots and UI observations can support claims about visible UI state, but they are not equivalent to official docs or source code for capability claims. Record them as `browser_screenshot` or `browser_observation`.

## Connector Evidence

App or MCP connector outputs may include private data. Use them only when authorized by the user or the task context. Record connector name, retrieval method, and privacy scope.

## Mutation Boundary

DeepSearch is read-first. Do not write files, run formatters, create artifacts, or mutate repos unless the user asks for durable output or implementation.

When writing is authorized:

- Announce target files before editing.
- Use `apply_patch` for manual edits.
- Keep generated research artifacts out of unrelated project repos.
- Never stage or commit automatically.
