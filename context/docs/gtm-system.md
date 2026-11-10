# PaidHR Outbound GTM System

**Status: DESIGN v0.1 (2026-11-10).** Nothing is built or connected yet. This doc is a work in progress.

**Built from:** context/icp/icp.md, personas.md, signal-matrix.md, context/messaging/facts.md and the starter-kit playbooks.

**Tools:** Claude Code, Clay, HubSpot, n8n, PlusVibe and GitHub were named in the brief. The research hasn't shown whether PaidHR uses any of them today, so they're the target stack, not a description of the current setup.

**Labels:**
- **Tags such as S1 and U1** refer to the segments and signals in context/icp/signal-matrix.md.
- **INFERRED** means a design choice not backed by research.
- **"Starting default"** means a threshold to replace once real data is in. It is not a known number.

**Miro board:** [PaidHR GTM System](https://miro.com/app/board/uXjVEP5xfS4=/) (created 2026-11-10). Source spec and local copy: `context/docs/diagrams/paidhr-gtm-system.json` and `.svg`.

---

## The flow at a glance

1. **Find and qualify accounts:** Context OS, then signals, find companies, enrich, ICP fit check, then route by segment.
2. **Pick the people and write the message:** find people, then find and verify emails, personalise, QA, then approval.
3. **Send, sort replies and learn:** sequence, reply handling, CRM, then the weekly loop back to the Context OS.

---

## 1. Context OS

| | |
|---|---|
| **What happens** | The source of truth for who we target and what we may say: ICP, personas, signal matrix, messaging and facts.md. Each workflow gets a spec (`/build-workflow-spec`), then copy (`/campaign-copy`) |
| **Tools** | Claude Code (skills), GitHub (version history, single source) |
| **Output** | `output/campaigns/<workflow>/workflow-spec.md`, marked STRUCTURE-APPROVED with copy appended |

| Decision | Answer | Leads to |
|---|---|---|
| Is facts.md approved? | No | Copy can only use `{{placeholders}}`; nothing ships |
| | Yes (approved 2026-11-10) | Copy may use approved claims and names |
| Is the sender set? | No (today: open question) | Blocker for steps 9 to 10 |
| | Yes | Signature and persona go into the sequence |
| Is the workflow spec STRUCTURE-APPROVED? | No | Back to `/build-workflow-spec` |
| | Yes | Build its Clay table (step 2) |

## 2. Buying signals (always on)

| | |
|---|---|
| **What happens** | Scheduled jobs catch signals and send them into Clay as rows. Every row keeps its signal ID, source URL and date |
| **Tools** | n8n (schedules, Apify runs, RSS), Clay (receives rows by webhook; runs Clay-native searches) |
| **Signals live first** | Build-first list from signal-matrix.md, below |

Build-first signals:

| Signal | Source | Runs |
|---|---|---|
| U1 HR and payroll hiring | Apify Jobberman scrape, run by n8n, sent to Clay by webhook | Weekly |
| N3 Frontline volume hiring | Same scrape, frontline keywords | Weekly |
| U3 New HR or Finance leader | Clay "Find People", start date within 90 days | Monthly |
| U5 Fresh funding | n8n RSS of funding roundups, plus Crunchbase via Clay | Weekly |
| U6 Annual return window | Calendar overlay, 1 Dec to 31 Jan | Yearly |

| Decision | Answer | Leads to |
|---|---|---|
| Is the signal fresh? (starting default: job posts 30 days or less, leader or funding 90 days or less) | No | Discard |
| | Yes | Step 3 |
| Is the company already in this workflow's table? | Yes | Add the signal to the existing row (stacked signals raise priority). No new row |
| | No | New row |

## 3. Find companies

| | |
|---|---|
| **What happens** | Turn the employer name from a job post or article into a company record: domain, LinkedIn page, HQ |
| **Tools** | Clay (company lookup, Claygent fallback) |

| Decision | Answer | Leads to |
|---|---|---|
| Is the poster the real employer? | No: recruitment agency or "confidential" (INFERRED: common on Nigerian job boards) | Drop |
| | Yes | Next check |
| Domain found? | No | Hold in an "unresolved" view, recheck once, then drop after 14 days (starting default) |
| | Yes | Step 4 |

## 4. Enrich

| | |
|---|---|
| **What happens** | Add the fields that the fit check and routing need |
| **Tools** | Clay (company enrichment, job-post fields, Claygent website read); n8n (PenCom list match, INFERRED build) |

| Field | Used by |
|---|---|
| Headcount, HQ country, industry | Fit check (step 5) |
| States and countries named in job posts | S3 routing, multi-state boost |
| Share of open roles that are frontline | S4 routing |
| HR, People or Finance title present | S5 vs S6 routing |
| Last funding date and round | S2 routing |
| Rival tool named in job posts (SeamlessHR, Workpay, PayDayNG) | S1 routing |
| Match on PenCom uncredited-remittance list | Priority flag only, never used in copy |

## 5. ICP fit check

| | |
|---|---|
| **What happens** | Apply the hard filters and the not-a-fit list from icp.md, then check HubSpot |
| **Tools** | Clay (formulas), HubSpot (lookup through the Clay integration) |

| Decision | Answer | Leads to |
|---|---|---|
| Runs payroll in Nigeria? | No | Drop. This includes foreign firms needing an Employer of Record (not a fit) |
| | Yes | Next check |
| 20+ staff? | Under 20 | Nurture. U4 headcount tracking brings it back at 20 |
| | Unknown (LinkedIn undercounts frontline staff, INFERRED) | Keep if the signal is U1 or N3 and flag "size unverified". Otherwise drop |
| | 20+ | Next check |
| In HubSpot? | Customer | Exclude; hand to the account manager as an expansion lead |
| | Open deal, or contacted in the last 90 days (starting default) | Exclude |
| | Closed-lost more than 6 months ago (starting default) | Allow; mark "reactivation" |
| | No | Step 6 |

## 6. Routing by segment

| | |
|---|---|
| **What happens** | Put each account in the first segment it matches, top to bottom (signal-matrix.md). The segment sets the angle and lead pillar |
| **Tools** | Clay (formula column) |

| Decision: which segment? | Rule | Lead pillar (messaging.md) |
|---|---|---|
| S1 Recent switchers | Rival tool in job posts, or on the ex-Bento list | Compliance and trust. Never name the rival |
| S2 Funded startups | Seed to Series B in the last 12 months | Payroll that scales with hiring |
| S3 Multi-location or cross-border | Posts in 2+ states, or in another country | Multi-state remittance, cross-border pay |
| S4 Frontline-heavy | Most open roles are frontline, 50+ staff | Retention through EWA |
| S5 HR-led SME | HR title present, 20 to 200 staff | One platform, fewer chases |
| S6 Owner-run SME | No HR, People or Finance title, 20 to 50 staff | Stop running payroll yourself (Famasi) |

| Decision | Answer | Leads to |
|---|---|---|
| Date between 1 Dec and 31 Jan? | Yes | Compliance pillar leads for every segment (annual return due 31 January) |
| | No | Segment pillar as above |
| On the PenCom list? | Yes | Send first (priority 1). Same copy |
| | No | Normal priority |

## 7. Find people

| | |
|---|---|
| **What happens** | Find up to 2 contacts per account (starting default), picked by segment from personas.md |
| **Tools** | Clay (Find People; Apollo or LinkedIn data) |

| Segment | Contact 1 | Contact 2 |
|---|---|---|
| S6 | CEO or founder | None |
| S2, S5 | HR or People lead (champion) | CEO or founder |
| Any segment with 100+ staff | HR or People lead | Finance lead or CFO (INFERRED buyer [pe]) |
| S3 | HR lead | Finance lead |
| S4 | HR lead | CEO, or COO for operations-heavy firms (INFERRED) |

| Decision | Answer | Leads to |
|---|---|---|
| Champion found? | No | Contact the economic buyer only |
| | Yes | Both contacts, with a 3-day gap between them (starting default) |
| Anyone found? | No | Park the account and retry at the next signal |

## 8. Find and verify emails

| | |
|---|---|
| **What happens** | Run several email-finding providers in turn, then verify the result |
| **Tools** | Clay (email waterfall plus verification) |

| Decision | Answer | Leads to |
|---|---|---|
| Is the email valid? | Valid | Email plus LinkedIn sequence |
| | Catch-all (accepts any address) | Lead with LinkedIn; email only from the lowest-risk inbox pool |
| | Invalid or not found | LinkedIn-only track |
| LinkedIn profile found? | No, and no valid email | Drop the contact |
| Is the contact already in HubSpot? | Yes, owned by a rep | Exclude; tell the owner |
| | No | Step 9 |

## 9. Sequence (email and LinkedIn)

| | |
|---|---|
| **What happens** | Clay fills each row's variables (signal, segment, angle, first line); the approved templates from `/campaign-copy` do the rest. Claude writes only the first line, within the facts.md rules. Batches go through QA, then human approval, then PlusVibe |
| **Tools** | Clay (variables, AI column), Claude Code (`/campaign-copy`, `/campaign-qa`, `/inbox-placement-test`), PlusVibe (email sending). LinkedIn sending: **no tool chosen yet** (gap) |
| **Shape** | 3 emails over about 10 days, plus a LinkedIn connect and 1 message (starting default, INFERRED). One sequence per segment and angle |

| Decision | Answer | Leads to |
|---|---|---|
| Does `/campaign-qa` pass? | No | Fix the variables or copy, then rerun QA |
| | Yes | Next check |
| Inbox placement OK? | No | Rest or replace the inboxes before sending (`/inbox-placement-test`) |
| | Yes | Next check |
| Approved by a human? (rule 4) | No | Hold |
| | Yes | PlusVibe sends; LinkedIn steps are queued |

## 10. Reply handling

| | |
|---|---|
| **What happens** | A PlusVibe reply webhook goes to n8n. Claude tags the intent, n8n acts and logs it in HubSpot |
| **Tools** | PlusVibe (webhook), n8n (routing), Claude (classification), HubSpot |

| Decision: reply type? | Leads to |
|---|---|
| Interested | HubSpot deal at "Meeting booked" or "Reply: interested"; alert the rep; stop the sequence for the whole account |
| Not now, with a date (for example "after annual returns") | HubSpot task on that date; pause |
| Wrong person, or a referral | Back to step 7 with the name given |
| Uses a rival or is happy with their setup | Tag the rival; nurture; re-eligible in 6 months (starting default) |
| Unsubscribe or hostile | Suppress in PlusVibe, HubSpot and Clay. Never contact again |
| Out of office | Pause until their return date, then resume |
| Bounce | Mark the email invalid; fall back to LinkedIn only |
| No reply after the last step | Back to the signal pool; re-eligible on a new signal after 90 days |

| Decision | Answer | Leads to |
|---|---|---|
| Is the tag confidence low? | Yes | A human reviews it in n8n before any action |
| | No | Automatic action |

## 11. CRM

| | |
|---|---|
| **What happens** | HubSpot holds the one record of every company, contact, deal and suppression. Every record carries properties so results can be traced back |
| **Tools** | HubSpot (Clay and n8n write to it) |
| **Properties** | `signal_id` (U1, N3...), `segment` (S1 to S6), `angle`, `workflow` (W1...), `campaign`, `sequence_step`, `first_touch_date` |
| **Deal stages** | Meeting booked, then Demo done, then Proposal, then Closed won or Closed lost. PaidHR's real stages aren't known (INFERRED) |

| Decision | Answer | Leads to |
|---|---|---|
| Deal outcome? | Closed won | Add to the lookalike seed list (N8) and the champion-tracking list (N9) |
| | Closed lost | Record the reason; reactivation eligible after 6 months |
| | Stalled 30 days or more (starting default) | Rep task; check that the champion is still active |

## 12. Weekly feedback loop

| | |
|---|---|
| **What happens** | Every Monday, n8n pulls PlusVibe and HubSpot stats by signal, segment and angle. Claude Code writes the week's learnings, updates the matrix, and commits to GitHub with a work-log entry |
| **Tools** | n8n (pull), Claude Code (analysis, edits), GitHub (commit), HubSpot and PlusVibe (data) |
| **Updates** | `knowledge-base/learnings/`, the V and R scores in signal-matrix.md (measured volume replaces guesses), proof in facts.md (new wins, for approval), personas.md (real objections from replies), the weekly priorities |

| Decision (per signal and angle) | Answer | Leads to |
|---|---|---|
| Enough sends to judge? (starting default: 200 per angle) | No | Keep running |
| | Yes | Next check |
| Meeting rate on target? (target to set with sales; unknown) | Yes | Scale: more keywords, more inboxes |
| | No, first or second try | New angle (`/campaign-copy` edit), same signal |
| | No, after two angle changes | Kill the signal; record why in learnings and the matrix |
| Bounce rate high? | Yes | Pause; check enrichment and email verification (step 8) |
| New objection seen 3+ times? | Yes | Add it to personas.md and the copy |

---

## Check against the four pillars

| Pillar | How the design meets it | Gaps |
|---|---|---|
| **Clean data** | One record in HubSpot. Dedupe at steps 2, 5 and 8. Every row keeps signal, source URL and date. Emails verified. Suppression shared across PlusVibe, HubSpot and Clay. Claims only from facts.md | PaidHR's customer list isn't loaded yet, so customers could be emailed. LinkedIn headcount is unreliable for frontline firms |
| **Always-on signals** | n8n schedules: Jobberman weekly, funding weekly, new leaders monthly, annual return window yearly. No manual list pulls | PenCom list format not checked. The champion-migration signal (N9) needs CRM data |
| **Composable workflows** | One Jobberman scrape feeds 5 signals. Steps 3 to 8 are the same Clay blocks for every workflow; only signal inputs and routing change. Skills are reusable (`/build-workflow-spec`, `/campaign-copy`, `/campaign-qa`) | No Clay table template saved yet (`/save-clay-schema` after the first approved table) |
| **Tight feedback loops** | Every send and reply is tagged with signal, segment and angle, so results trace back. Weekly review changes the matrix, copy and personas, with kill rules | Meeting-rate target not set. No baseline until W1 has run for a few weeks |

## Blockers before the first send

1. A sender chosen (facts.md claims approved 2026-11-10).
2. Clay, HubSpot, n8n and PlusVibe accounts connected. None are configured in `tools/` or `.env` yet.
3. A LinkedIn sending tool chosen.
4. PaidHR's customer and open-deal list loaded into HubSpot for exclusion.
5. Meeting-rate target agreed with sales.
