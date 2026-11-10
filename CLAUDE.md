# PaidHR GTM Context OS

## Company
PaidHR (paidhr.com, formerly Pade HCM): Lagos-based HR and payroll platform for African businesses, Nigeria first, with payroll, automatic PAYE and pension remittance, cross-border pay and employee finance (EWA, Loan Marketplace); $1.8M seed led by Accion Venture Lab, 2025. Source: context/docs/research/company.md.

## How this folder works
- `.claude/skills/`: reusable Claude skills for repeat GTM tasks. Read when a task matches a skill.
- `context/icp/`: `icp.md` (five-layer ICP, not-a-fit), `personas.md` (champion, economic buyer, influencer), `signal-matrix.md` (segments x personas, signals, build order). Read before any targeting, list building or copy.
- `context/positioning/`: `positioning.md`, `value-proposition.md`, `competitors.md`. Read before writing messaging or comparing PaidHR to others.
- `context/messaging/`: `messaging.md` (core message, pillars, angles, words), `facts.md` (the only source of names, numbers and claims for copy). Read before writing any copy.
- `context/brand-kit/`: `brand.md` (tone and key phrases from PaidHR copy). Read before producing anything customer facing.
- `context/docs/`: `case-studies.md` (every customer story with source). Read before citing a customer.
- `context/docs/research/`: raw research notes with sources (company, customers, customer-videos, competitors, market, signals, voice). Read when you need to verify or cite a company fact.
- `knowledge-base/playbooks/`: step by step GTM workflows. Read before running or speccing a workflow.
- `knowledge-base/learnings/`: what worked, what didn't, and why. Read before planning a new campaign.
- `meetings/`: meeting notes and transcripts. Read when a task references a past conversation.
- `output/campaigns/`: finished campaign assets and copy. Write final campaign deliverables here.
- `output/outbound/`: outbound sequences, emails and LinkedIn messages. Write outbound copy here.
- `output/social/`: social posts and content. Write social deliverables here.
- `output/data/`: lists, enrichment outputs and exports (CSV and XLSX stay gitignored). Write data deliverables here.
- `inspiration/`: ads and examples to learn from. Read when writing copy or designing a campaign for reference, never copy verbatim.
- `tools/`: scripts and tool configs for the GTM stack. Read before automating anything.
- `weekly-priorities/`: one file per ISO week with that week's priorities. Read at the start of every session.
- `work-log/`: one file per ISO week logging every change. Append to this week's file after every change.

## Rules
1. Cite a source (URL or file path) for every company fact.
2. Never invent numbers. If a figure isn't sourced, say it's unknown.
3. No em dashes in any copy.
4. Ask before sending or publishing anything.
5. Log every change in this week's work log (`work-log/YYYY-Www.md`) with a timestamp.

## Tools
- Miro (MCP, via the miro plugin): for diagrams, such as GTM system maps and workflow flows.
- Notion (MCP): where we publish finished docs. GitHub stays the source of truth, so edit here first, then publish to Notion (ask first, per rule 4).
- Google Workspace CLI (`gws`, see `tools/gws/README.md`): read and write Sheets, Drive, Docs, Gmail and Calendar from the terminal. Use `--dry-run` and ask before anything that sends or shares.

## Skills
From github.com/bolaji-ships/gtm-starter-kit. Each lives in `.claude/skills/<name>/SKILL.md`.
- Research to copy, in order: `campaign-strategy`, `signal-matrix`, `build-workflow-spec`, `campaign-copy`, then `miro-gtm-flowchart` to draw the system.
- Clay builds (use `tools/rex`): `build-clay`, `prompt-builder`, `campaign-contract`, `design-clay-table-json`, `import-clay-table`, `save-clay-schema`.
- Clay costs and data: `calculate-costs`, `workspace-cost-audit`, `export-tables`. Pre-launch QA: `campaign-qa`.
- Research and deliverability: `crawl4ai`, `agent-browser`, `inbox-placement-test`.
