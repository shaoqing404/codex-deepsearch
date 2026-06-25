# Spec 002: Forward Test Plan

## Purpose

Forward-test whether `codex-deepsearch` changes Codex behavior from broad summarization to evidence-led research with reviewable claims.

## Test Prompts

1. Current product/API capability:

   ```text
   Use $codex-deepsearch to determine whether Codex skills can be installed as symlinked folders and whether that is suitable for local development.
   ```

2. Implementation-prep research:

   ```text
   Use $codex-deepsearch to research whether this repo's planned feature should become an implementation spec. Separate local code evidence from public docs.
   ```

3. Optional delegation:

   ```text
   Use $codex-deepsearch. If codex-with-cc-plus is available, use delegated researcher/reviewer workers to widen the search and run a skeptic review before synthesis.
   ```

## Expected Behavior

- Research design appears before searching.
- Scenario matrix is present.
- Snippet-only sources are labeled correctly.
- Source ledger and claim ledger exist before synthesis.
- Tool limits are disclosed.
- Review gate decides whether the output can become spec/roadmap/implementation input.

## Failure Signals

- Link list without claim ledger.
- Confident claims backed only by snippets.
- No counter-evidence pass.
- Worker report accepted without main-thread review.
- Private/ignored local files read without authorization.
