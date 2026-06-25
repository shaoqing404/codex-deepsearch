# Review Gate

Run this gate before accepting any Codex DeepSearch report, worker report, or synthesis.

## Reject As Not DeepSearch

Reject or request rework when:

- There is no research design.
- There is no scenario matrix.
- There is no source ledger.
- There is no claim ledger.
- Major claims cite only snippets but are labeled `retrieved_fact`.
- The synthesis appears before evidence audit.
- Sources are listed but not mapped to claims.
- There is no counter-evidence search.
- Tool limitations are hidden.
- Local/private evidence was used without authorization.
- The conclusion does not answer the decision question.

## Source Quality Checks

For each high-impact claim:

1. Is there a primary or official source?
2. Was the source opened/read/rendered, or only seen through a snippet/summary?
3. Is the source current enough for the decision?
4. Is there conflicting evidence?
5. Does the claim depend on local/manual validation?
6. Does the decision change if the claim is false?

## Scenario Quality Checks

Confirm the report separated cases that change the answer:

- Role or permission.
- Product plan or edition.
- OS/runtime/framework/version.
- Region/legal/policy regime.
- Cloud versus local execution.
- Admin versus ordinary user.
- Official support versus workaround.
- Feasibility versus recommendation.

## Confidence Calibration

Use:

- `high`: opened/read primary evidence, current enough, counter-search found no material conflict.
- `medium`: credible but incomplete evidence, one-hop inference, or one important assumption.
- `low`: snippet-only, stale, untested local behavior, community-only, or materially conflicted.

Never accept high confidence from snippet-only evidence.

## Goal Completion Gate

In `/goal` mode, completion requires:

- Research design accepted.
- Scenario matrix accepted.
- Ledgers complete enough for the decision.
- Counter-evidence attempted for major conclusions.
- Synthesis traceable to ledger rows.
- Remaining gaps explicitly listed.
- Readiness decision made.

If any item fails, do not mark the goal complete; report `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, or `BLOCKED`.

## Readiness Decision

Answer:

```text
Accepted: yes/no
Reason:
Missing Evidence:
Overstated Claims:
Snippet-Only Claims:
Counter-Evidence Gaps:
Privacy Or Repo Safety Issues:
Required Rework:
Can become spec: yes/no
Can become roadmap input: yes/no
Can become implementation input: yes/no
Status: DONE | DONE_WITH_CONCERNS | NEEDS_CONTEXT | BLOCKED
```

If readiness is `no`, name the smallest next check that could change it.
