# Privacy And Repo Safety

Use this reference before local file inspection, artifact creation, delegation, or final handoff.

## Default Private Boundaries

Do not read or upload these unless explicitly authorized for the current task:

- `workspace/`
- `recordings/`
- `transcripts/`
- `tts/`
- `audio/`
- `.env`, `.env.*`, secrets, credentials, tokens, keys
- private resumes, salary records, interview logs, recruiting communication
- local databases
- private chat exports
- ignored files and directories
- files with names that clearly indicate personal or confidential material

If a repo-specific `AGENTS.md` names additional private paths, follow it.

## Before Reading Local Files

1. Identify the repo/workspace root.
2. Check `.gitignore` if broad inspection could cross ignored paths.
3. Use targeted `rg --files` or `rg` patterns.
4. Avoid opening binary, database, audio, transcript, or private export files.
5. Record local file reads in the source ledger.

## Before Writing Artifacts

1. Confirm the user asked for durable output.
2. Choose an authorized output directory.
3. Run `git status --short` in the target repo if it is version-controlled.
4. Avoid writing research artifacts into unrelated project repos.
5. Use `apply_patch` for manual file creation or edits.

## Git Safety

- Never use `git add .`.
- Never commit, push, reset, checkout, or clean unless explicitly asked.
- Do not revert user changes.
- If changes already exist in touched files, read them and work with them.
- Ignore unrelated dirty files.

## Delegation Safety

Task files for workers must state:

- Allowed local paths.
- Forbidden local paths.
- Whether private files are authorized.
- No upload rule.
- No git mutation rule.
- Report of any denied or skipped private source.

Workers that read private or ignored material outside scope must be rejected.

## External Tools And Uploads

Do not paste private local content into web pages, external APIs, public issue trackers, or search engines. Connector access must be user-authorized and recorded as connector evidence.

For public web research, search queries should avoid exposing private names, private filenames, private company records, internal URLs, secrets, or unique personal details unless the user explicitly instructs otherwise.
