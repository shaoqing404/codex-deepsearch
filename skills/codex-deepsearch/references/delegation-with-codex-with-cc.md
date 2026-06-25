# Delegation With Codex With CC

Use this reference only when the user explicitly asks for subagents, delegation, worker execution, `codex-with-cc`, Claude Code, or when the user permits optional parallel research to widen search and analysis.

`codex-with-cc-plus` is optional. Codex DeepSearch must still work without it.

## Roles

Main Codex:

- Owns research design.
- Defines scenario matrix.
- Writes or approves task files.
- Reviews source and claim ledgers.
- Runs the review gate.
- Produces final synthesis and readiness decision.

Workers:

- Source scout: discover and open primary sources; fill source ledger.
- Scenario analyst: expand scenario matrix and map claims.
- Skeptic reviewer: find counter-evidence, stale claims, unsupported cases, snippet-only claims, and overconfident inferences.
- Synthesizer: draft synthesis from accepted ledgers only.

Workers do not decide final acceptance.

## When To Delegate

Delegate when:

- The topic is broad enough for parallel source discovery.
- Multiple domains need independent review.
- The output may become a spec, roadmap, product decision, or implementation input.
- The user explicitly asks for a subagent/worker/delegated workflow.

Do not delegate when:

- The question is small enough for one Codex pass.
- Scope or private-data authorization is unclear.
- Workers would need to read private/ignored materials without explicit permission.
- The available worker system cannot open sources or report limitations.

## TaskFile Additions

Add this to `Goal`:

```text
Execute Codex DeepSearch, not broad summarization. Build Research Design, Scenario Matrix, Source Ledger, Claim Ledger, Counter-Evidence, Synthesis, Verification Gaps, Recommended Next Checks, and Review Gate notes. Do not synthesize until ledgers exist.
```

Add this to `Allowed Scope`:

```text
Use public web/search/open tools and explicitly authorized local files for source discovery. Prefer official docs, source repositories, standards, laws, API docs, changelogs, release notes, and primary materials. Use blogs only for operational details and mark them lower confidence.
```

Add this to `Forbidden Actions`:

```text
Do not treat search snippets as retrieved facts.
Do not produce a link list without a claim ledger.
Do not use generated reasoning as a source.
Do not hide tool limitations.
Do not write final recommendations before counter-evidence search.
Do not broaden beyond the assigned scenario.
Do not read private or ignored project material unless explicitly authorized in the task file.
Do not edit project files, stage, commit, push, or upload private materials.
```

Add this to `Acceptance Criteria`:

```text
- Research Design includes decision question, audience, scope, exclusions, source priority, queries, and stop conditions.
- Scenario Matrix covers assigned cases that materially change the answer.
- Source Ledger includes URL/path, access date, source date when visible, source type, retrieval method, evidence scope, confidence, and limitations.
- Claim Ledger maps every material claim to source ids, evidence, counter-evidence, label, confidence, and decision impact.
- Snippet-only claims are labeled source_summary or needs_verification.
- Counter-Evidence lists what was searched and what changed.
- Synthesis is traceable to accepted ledger rows.
- Verification Gaps lists unresolved claims and manual/local checks.
```

Add this to `Verification`:

```text
- Which search/fetch/browser/MCP tools were available.
- Whether MiniMax MCP web_search was available.
- Whether WebFetch or equivalent full-page open was available.
- Whether full pages were opened or only snippets were available.
- Number of primary/official sources opened.
- Number of snippet-only sources used.
- Number of claim rows.
- Number of counter-evidence searches.
- Whether private/ignored materials were avoided.
```

## Report Requirements

Inside `Findings`, require these headings:

```text
Research Design
Scenario Matrix
Source Ledger
Claim Ledger
Counter-Evidence
Synthesis
Verification Gaps
Recommended Next Checks
Review Gate Notes
```

Status guidance:

- `DONE`: primary sources opened and material claims supported.
- `DONE_WITH_CONCERNS`: useful work but snippet-only, tool-limited, stale, or requires manual validation.
- `NEEDS_CONTEXT`: decision question, scenario, or authorization cannot be defined.
- `BLOCKED`: no useful source discovery or permitted evidence access.

## Expanding Search And Analysis

If the target user has `codex-with-cc-plus`, use it to widen research without weakening review:

- Split official-source discovery, implementation-source discovery, counter-evidence, and review into separate researcher/reviewer tasks.
- Keep worker scopes read-only unless the user explicitly asks for artifacts.
- Require workers to report tool availability, including MiniMax MCP and WebFetch availability.
- Main Codex merges ledgers and rejects duplicate, snippet-only, or unsupported claims.
- Add a skeptic reviewer before any synthesis becomes spec or implementation input.

If worker tooling is unavailable, record it as a limitation and continue with single-thread Codex DeepSearch when feasible.
