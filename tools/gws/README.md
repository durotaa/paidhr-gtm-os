# gws: Google Workspace CLI

One CLI for Drive, Sheets, Docs, Gmail, Calendar, Slides, Forms, Chat and the rest of Google Workspace. Returns structured JSON, so Claude can read and write Workspace files from this repo.

- Source: https://github.com/googleworkspace/cli (Apache-2.0; "not an officially supported Google product")
- Installed: 0.22.5 via Homebrew (`brew install googleworkspace-cli`), binary at `/opt/homebrew/bin/gws`
- Update: `brew upgrade googleworkspace-cli`. Pre-1.0, so expect breaking changes.

## Use in this repo

| Task | Command |
|---|---|
| Push a list to a Sheet | `gws sheets +append` / `gws sheets spreadsheets values append` |
| Read a Sheet | `gws sheets +read` |
| Upload a file to Drive | `gws drive +upload <file>` |
| List recent Drive files | `gws drive files list --params '{"pageSize": 10}'` |
| Append text to a Doc | `gws docs +write` |
| Preview any call without running it | add `--dry-run` |
| See a method's schema | `gws schema drive.files.list` |

Rules:
- Wrap Sheets ranges in single quotes (`'Sheet1!A1:C10'`) so the shell leaves `!` alone.
- Anything that sends, shares or publishes (`gmail +send`, `+reply`, `+forward`, `chat +send`, Drive permission changes, `workflow +file-announce`) needs a yes first (CLAUDE.md rule 4). Use `--dry-run` to show the request.
- GitHub stays the source of truth for docs. Sheets and Drive are for lists and handoffs.

## Current setup (2026-11-10)

- Logged in with a personal Google account (check with `gws auth status`), Google Cloud project `paidhr-gtm-os-gws`.
- Services: Drive, Sheets, Docs, Gmail, Calendar (25 scopes, including Gmail send and settings).
- External app in testing mode: if calls start failing with an auth error, rerun `gws auth login -s drive,sheets,docs,gmail,calendar`.
- Check: `gws auth status`.

## Auth (one time, done by you)

Credentials are stored outside the repo in `~/.config/gws/`, encrypted with the key in the macOS keychain. Never copy them into this folder.

`gcloud` is not installed, so use the manual setup:
1. In Google Cloud Console, create or pick a project and enable the APIs you need (Drive, Sheets, Docs, Gmail, Calendar).
2. OAuth consent screen: External, testing mode. Add your Google account under **Test users**.
3. Credentials: create an OAuth client of type **Desktop app**. Download the JSON to `~/.config/gws/client_secret.json`.
4. Run `gws auth login -s drive,sheets,docs,gmail,calendar`. Pick services: unverified apps fail with the full preset (about 25-scope limit).
5. Check with `gws auth status`.

Alternative: install `gcloud` (`brew install --cask google-cloud-sdk`), then `gws auth setup` creates the project and client for you.

## Agent skills

The repo ships about 95 SKILL.md files (one per API, helpers, personas, recipes). Not imported yet. To add some, copy from `skills/gws-*` in the source repo into `.claude/skills/`.
