# PaidHR GTM Context OS

## Company
PaidHR (paidhr.com, formerly Pade HCM): Lagos-based HR and payroll platform for African businesses, Nigeria first, with payroll, automatic PAYE and pension remittance, cross-border pay and employee finance (EWA, Loan Marketplace); $1.8M seed led by Accion Venture Lab, 2025. Source: context/docs/research/company.md.

## How this folder works
- Root files: `README.md` (public disclaimer: educational, not affiliated with PaidHR), `.gitignore` (keeps `.env`, CSV, XLSX and Google credentials out of Git), `.env` (local secrets, never committed), `.mcp.json` (Notion MCP server), `.claude/settings.json` (enables the Miro plugin).
- `.claude/skills/`: reusable Claude skills for repeat GTM tasks (18, listed under Skills). Read when a task matches a skill.
- `context/icp/`: `icp.md` (five-layer ICP, not-a-fit), `personas.md` (champion, economic buyer, influencer), `signal-matrix.md` (segments x personas, signals, build order). Read before any targeting, list building or copy.
- `context/positioning/`: `positioning.md`, `value-proposition.md`, `competitors.md`. Read before writing messaging or comparing PaidHR to others.
- `context/messaging/`: `messaging.md` (core message, pillars, angles, words), `facts.md` (the only source of names, numbers and claims for copy). Read before writing any copy.
- `context/brand-kit/`: `brand.md` (tone and key phrases from PaidHR copy). Read before producing anything customer facing.
- `context/docs/`: `case-studies.md` (every customer story with source), `gtm-system.md` (outbound system design, steps, tools, decisions). Read before citing a customer or building a workflow.
- `context/docs/diagrams/`: `paidhr-gtm-system.json` (flowchart spec), `paidhr-gtm-system.svg` and `paidhr-gtm-system.png` (the chart). The editable chart is the Miro board linked in `gtm-system.md`.
- `context/docs/research/`: raw research notes with sources: `company.md`, `customers.md`, `customer-videos.md`, `competitors.md`, `market.md`, `signals.md`, `voice.md`. Read when you need to verify or cite a company fact.
- `knowledge-base/playbooks/`: step by step GTM workflows. Read before running or speccing a workflow.
  - `workflow-anatomy.md` (Mother Intent Catalog, signal tests), `signal-matrix-framework.md`
  - Copy: `copy-iron-laws.md`, `copy-frameworks.md`, `copy-bans.yaml`, `linkedin-dm-frameworks.md`, `templates/facts-template.md`
  - Clay: `clay/expert.md`, `clay/iron-laws.md`, `clay/formulas.md`, `clay/prompts.md`, `clay/actions-data-credits.md`
- `knowledge-base/learnings/`: what worked, what didn't, and why (empty so far). Read before planning a new campaign.
- `meetings/`: meeting notes and transcripts (empty so far). Read when a task references a past conversation.
- `output/campaigns/`: finished campaign assets and copy. Write final campaign deliverables here.
  - `campaign-strategy.md`: 21 outbound ideas ranked by signal strength and data ease, with the recommended first build.
  - `hr-and-payroll-hire/workflow-spec.md`: workflow W1 (HR and payroll hire), structure and copy approved (3 emails, 2 LinkedIn DMs).
- `output/outbound/`: outbound sequences, emails and LinkedIn messages (empty so far). Write outbound copy here.
- `output/social/`: social posts and content (empty so far). Write social deliverables here.
- `output/data/`: lists, enrichment outputs and exports (empty so far; CSV and XLSX stay gitignored). Write data deliverables here.
- `inspiration/`: ads and examples to learn from (empty so far). Read when writing copy or designing a campaign for reference, never copy verbatim.
- `tools/`: scripts and tool configs for the GTM stack (each listed under Tools). Read before automating anything.
- `weekly-priorities/`: one file per ISO week with that week's priorities (current: `2026-W46.md`). Read at the start of every session.
- `work-log/`: one file per ISO week logging every change (current: `2026-W46.md`). Append to this week's file after every change.

## Rules
1. Cite a source (URL or file path) for every company fact.
2. Never invent numbers. If a figure isn't sourced, say it's unknown.
3. No em dashes in any copy.
4. Ask before sending or publishing anything.
5. Log every change in this week's work log (`work-log/YYYY-Www.md`) with a timestamp.

## Tools
- Miro (MCP, via the miro plugin): for diagrams, such as GTM system maps and workflow flows.
- Notion (MCP): where we publish finished docs. GitHub stays the source of truth, so edit here first, then publish to Notion (ask first, per rule 4). Published Context OS: [PaidHR GTM OS](https://app.notion.com/p/415795dde8a681b69e3fdc480dc047ab) (Context and Campaigns pages mirror `context/` and `output/campaigns/`; raw research is not published).
- Google Workspace CLI (`gws`, see `tools/gws/README.md`): read and write Sheets, Drive, Docs, Gmail and Calendar from the terminal. Use `--dry-run` and ask before anything that sends or shares.
- GitHub (`git` and the `gh` CLI): the source of truth, at github.com/durotaa/paidhr-gtm-os (public). Scan for secrets and personal details before every commit.
- Rex (`tools/rex/`): unofficial Clay client that works through your browser session. The Clay skills use it. Setup in `tools/rex/GETTING_STARTED.md`.
- crawl4ai (`tools/crawl4ai/README.md`): free local crawler that turns web pages into Markdown or JSON.
- agent-browser (`tools/agent-browser/README.md`): a browser Claude Code can drive, for sites that need clicks, forms or logins.
- Planned, not connected yet (target stack in `context/docs/gtm-system.md`): Clay (enrichment and tables), Apify (job board scrapes), n8n (schedules and webhooks), HubSpot (CRM), PlusVibe (email sending), and a LinkedIn sending tool (not chosen).

## Skills
From github.com/bolaji-ships/gtm-starter-kit. Each lives in `.claude/skills/<name>/SKILL.md`.
- Research to copy, in order: `campaign-strategy`, `signal-matrix`, `build-workflow-spec`, `campaign-copy`, then `miro-gtm-flowchart` to draw the system.
- Clay builds (use `tools/rex`): `build-clay`, `prompt-builder`, `campaign-contract`, `design-clay-table-json`, `import-clay-table`, `save-clay-schema`.
- Clay costs and data: `calculate-costs`, `workspace-cost-audit`, `export-tables`. Pre-launch QA: `campaign-qa`.
- Research and deliverability: `crawl4ai`, `agent-browser`, `inbox-placement-test`.
