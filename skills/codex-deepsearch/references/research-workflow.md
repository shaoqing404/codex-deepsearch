# Research Workflow

Use this workflow for source-backed research that may influence product, architecture, roadmap, implementation, or user-facing recommendations.

## 1. Frame

Before searching, write a short research design:

- Decision question.
- What the answer will let the user decide.
- Audience.
- Scope and exclusions.
- Privacy boundaries.
- Source priority.
- Required freshness.
- Stop conditions.

If these cannot be defined, return `NEEDS_CONTEXT`.

## 2. Scenario Matrix

Split the answer across cases that materially change the conclusion, such as:

- User role or permission.
- Product plan or edition.
- Operating system, runtime, framework, or version.
- Region, legal regime, or policy boundary.
- Local versus cloud execution.
- Prototype versus production implementation.
- Official support versus community workaround.

Avoid one generic answer when the correct answer depends on scenario.

## 3. Source Discovery

Search in passes:

1. Official or primary sources.
2. Source code, standards, changelogs, release notes, API docs, specs, filings, or papers.
3. Implementation reports, issue trackers, engineering blogs, and operational notes.
4. Counter-evidence: limitations, deprecations, unsupported cases, failures, privacy risk, stale docs.
5. Freshness check for current or unstable facts.

Record search limitations immediately.

## 4. Ledgers

Fill the source ledger while searching. Fill the claim ledger before synthesis.

Every material claim in the synthesis must map to source ids, a label, confidence, counter-evidence, and decision impact. Remove or downgrade unsupported claims.

## 5. Counter-Evidence

For each major conclusion, run at least one anti-claim check. For legal, medical, financial, security, privacy, product capability, model behavior, or API availability topics, counter-evidence search is mandatory.

Useful counter-query shapes:

- `<claim keywords> limitation`
- `<claim keywords> deprecated`
- `<claim keywords> not supported`
- `<claim keywords> privacy risk`
- `<claim keywords> changelog`
- `<claim keywords> site:github.com issues`

## 6. Synthesis

Synthesize only after ledgers exist.

Separate:

- Retrieved facts.
- Source summaries.
- Inferences.
- Recommendations.
- Verification gaps.

Start with the practical conclusion, then show why it follows. State what would change the answer.

## 7. Review

Run `references/review-gate.md`.

The review decision must include:

- Accepted: yes/no.
- Missing evidence.
- Overstated claims.
- Snippet-only claims.
- Counter-evidence gaps.
- Required rework.
- Can become spec/roadmap/implementation input: yes/no.

## 8. Handoff

Use `DONE` only if evidence and review support it. Otherwise use `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, or `BLOCKED`.

For implementation handoff, include:

- Stable facts.
- Assumptions to preserve.
- Decisions still needed.
- Interfaces or constraints affected.
- Verification required before coding.
