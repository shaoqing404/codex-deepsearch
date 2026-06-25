# Source And Claim Ledgers

Use ledgers to prevent DeepSearch from becoming a link list or a confident narrative without evidence.

## Source Ledger

Every source used in synthesis needs a row:

| source_id | title | url_or_path | access_date | source_date | source_type | retrieval_method | evidence_scope | confidence | limitations |
|---|---|---|---|---|---|---|---|---|---|

`source_type` examples:

- official_docs
- official_help_center
- standards_or_law
- source_code
- github_readme
- changelog_or_release_notes
- academic_paper
- company_blog
- engineering_blog
- community_forum
- issue_tracker
- search_snippet
- local_project_file
- user_provided
- connector_private_data

`retrieval_method` examples:

- opened_full_page
- web_search_snippet
- browser_screenshot
- local_file_read
- pdf_rendered
- api_result
- mcp_connector_result
- user_provided
- worker_report

`evidence_scope` examples:

- public_web
- official_public
- local_repo
- local_private_authorized
- user_provided_private
- connector_authorized
- snippet_only

Rules:

- Search snippets are discovery only. Mark source type `search_snippet` or retrieval method `web_search_snippet`.
- A blocked, paywalled, login-only, region-blocked, or snippet-only source cannot support high confidence by itself.
- A source with unknown date can be used, but mark `source_date=unknown`.
- Local private or connector data must be explicitly authorized and labeled.
- Worker reports are not primary sources; they are summaries of evidence that still need ledger rows for the underlying sources.

## Claim Ledger

Every material claim needs a row:

| claim_id | claim | label | supporting_sources | direct_evidence | counter_evidence | assumptions | confidence | decision_impact | next_check |
|---|---|---|---|---|---|---|---|---|---|

Labels:

- `retrieved_fact`: Directly supported by a source that was opened, rendered, fetched, read locally, or retrieved through an authorized connector.
- `source_summary`: Supported only by search snippets, abstracts, catalog metadata, tool summaries, or worker summaries.
- `inference`: Reasoned interpretation based on retrieved facts.
- `needs_verification`: Plausible but unverified, tool-limited, stale, or dependent on manual/local checks.
- `conflict`: Materially contested by another source.

Confidence:

- `high`: Primary or official source opened, current enough, no material conflict after counter-search.
- `medium`: Credible source but partial coverage, one-hop inference, limited freshness, or unresolved assumption.
- `low`: Snippet-only, community-only, stale, tool-limited, or materially conflicted.

Rules:

- One claim per row.
- Do not mix facts and recommendations in one claim.
- Do not use generated reasoning as a source.
- Do not give high confidence to snippet-only evidence.
- Include counter-evidence even when it does not overturn the claim.
- If no counter-search was attempted, say so in `next_check`.
