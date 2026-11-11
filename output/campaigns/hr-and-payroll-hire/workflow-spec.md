# Workflow Spec: HR and Payroll Hire

**Status:** STRUCTURE-APPROVED 2026-11-10 · COPY-APPROVED 2026-11-11

**Built from:**
- output/campaigns/campaign-strategy.md (idea 2, with ideas 1, 3 and 5 folded in)
- context/icp/ (icp.md, personas.md, signal-matrix.md)
- context/docs/gtm-system.md
- context/messaging/facts.md

**Source tags:**

| Tag | File |
|---|---|
| [sm] | context/icp/signal-matrix.md |
| [gs] | context/docs/gtm-system.md |
| [fa] | context/messaging/facts.md |
| [icp] | context/icp/icp.md |

`INFERRED` means a design choice not backed by research.

**Workflow tracker:** W1 in signal-matrix.md.

---

## 1. Mother intent [ENGINE]

**A Nigerian employer has posted a job for an HR or payroll role in the last 30 days.**

- **Catalog match:** Hiring specific roles (knowledge-base/playbooks/workflow-anatomy.md).
- **Signal-matrix ID:** U1, scored 17 out of 20 [sm].

## 2. Inclusion and exclusion [ICP]

### Include: the ICP box [icp]

| Filter | Rule | How it's checked |
|---|---|---|
| Payroll in Nigeria | Job location is in Nigeria and the company's HQ country is Nigeria | Location field on the job post; Clay company HQ |
| Size | 20+ staff on LinkedIn | Clay company headcount |
| Size unknown | Keep, and flag `size_unverified` | [gs] step 5: LinkedIn undercounts frontline staff |
| Industry | Any. The industry list in icp.md is "claimed, not proven" | None |

### Include: the trigger definition

| Field | Rule |
|---|---|
| Titles that match | HR Manager, HR Generalist, HR Officer, HR & Admin Officer or Manager, Human Resources Manager, People Operations or People Lead, Head of HR or People, Payroll Officer, Payroll Specialist, Payroll Accountant, HR and Payroll Officer |
| Titles that don't count | Intern, NYSC, graduate trainee, recruiter, talent acquisition, HR Assistant (INFERRED: too junior to own payroll) |
| Freshness | Posted in the last 30 days |
| Duplicates | One row per company. More posts add to that row, they don't create new rows |

### Include: who we contact

Set by routing cell (section 5), from [gs] step 7:
- **Cells A and B:** the CEO or founder only.
- **Cells C and D:** the HR or People lead, then a second contact 3 days later. The second contact is the CEO, or the Finance lead or CFO at companies with 100+ staff.
- **Never:** the person being hired.

### Exclude

| Who | Why | How it's read |
|---|---|---|
| Recruitment agencies and "confidential" posters | The real employer is unknown | Poster name matches agency keywords (recruit, staffing, outsourcing, consulting, "HR solutions"), or the employer field says "confidential" |
| Payroll bureaus and HR consultancies | Partner audience (strategy idea 12), not a buyer here | Same keyword match, plus Clay industry |
| HR software companies (SeamlessHR, Workpay, PayDayNG, others) and PaidHR | Competitors | Name blocklist, plus Clay industry "HR software" |
| Government and public bodies | INFERRED: payroll runs through state systems. Not in the research | Clay industry "Government Administration" |
| Under 20 staff | Below PaidHR's lowest price tier | Headcount under 20. These go to nurture, not drop |
| HubSpot: customer, open deal, or contacted in the last 90 days | [gs] step 5 | HubSpot lookup in Clay |
| Contact already owned by a rep | [gs] step 8 | HubSpot contact owner |

## 3. Sources [ENGINE]

| Purpose | Source | Tool | Runs |
|---|---|---|---|
| **Trigger** | Jobberman and MyJobMag | Apify Jobberman actor and Africa Jobs Aggregator actor, about $1 per 1,000 results [sm]. n8n runs them and sends rows to Clay by webhook | Weekly |
| **Trigger** | LinkedIn Jobs, Nigeria | Apify LinkedIn Jobs actor (INFERRED: not yet checked) | Weekly |
| Employer to domain and LinkedIn page | Job post employer name | Clay company lookup, with Claygent as fallback | Per row |
| Headcount, HQ, industry | LinkedIn company page | Clay Enrich Company | Per row |
| HR titles at the company, and the contacts | LinkedIn people data | Clay Find People (Apollo or LinkedIn data) | Per row |
| Job description text | The same job post | Apify output field `description` | Per row |
| Funding | Crunchbase | Clay Find Organization (Crunchbase) | Per row |
| Customers, open deals, recent contacts | HubSpot | Clay HubSpot lookup | Per row |
| Emails | Email providers | Clay email waterfall plus verification | Per contact |
| Priority flag | PenCom list of employers with uncredited remittances | n8n or crawl4ai scrape, then a name match (INFERRED build; page format not checked [sm]) | Monthly |

## 4. Signals table [ENGINE]

| # | Signal | Role | How it's read | Output |
|---|---|---|---|---|
| T1 | HR or payroll job posted in Nigeria, 30 days or less | **trigger** | Regex on job title (the title list in section 2, minus the excluded words), plus location in Nigeria, plus posted date 30 days ago or later | true / false |
| R1 | HR team already exists | **router** | Count of current employees in HR or People titles, from Clay Find People, not counting the posted role | Clusters: **0 = no HR team**; **1+ = HR team exists**. Raw counts never go to copy |
| R2 | Role family | **router** | Regex on job title. The title contains "payroll" → **payroll role**. Otherwise → **HR generalist role**. "HR and Payroll Officer" counts as payroll | payroll / generalist |
| C1 | Remittance duties in the job description | **context-clause** | Keyword match on the description: PAYE, pension, remittance, NHF, NSITF, "tax returns" | Enum: `paye`, `pension`, `remittance`, `none`. Never routes |
| C2 | Annual return window | **context-clause** | Send date between 1 Dec and 31 Jan | true / false |
| C3 | Jobs in 2+ Nigerian states | **context-clause** | Count of distinct states across the company's job posts | Clusters: **1 state = single site**; **2+ = multi-state** |
| C4 | Raised funding in the last 12 months | **context-clause** | Crunchbase last funding date within 365 days | true / false, plus round type |
| C5 | Several roles open | **context-clause** | Count of the company's job posts in the last 60 days | Clusters: **1 to 4 = normal**; **5+ = hiring fast** |

**Not narrative.** These reads filter or set priority only. They never route the message and never reach copy:
- real employer (not an agency)
- headcount 20+
- HubSpot status
- PenCom list match (send first, never mentioned [fa])
- rival tool named in the job description (logged for workflow W14, unused here)

**Why segments don't route here:**
- **S1 to S6 from the signal matrix:** a company hiring for HR shares one situation whatever its segment.
- **Funding (S2) and multi-state (S3):** these appear as context lines C4 and C3.
- **Frontline-heavy companies (S4):** they stay in this workflow when they post an HR role. Their volume hiring runs separately as W4.

## 5. Routing matrix with angles [ENGINE]

**How the grid is built:**
- **R1:** 2 clusters (no HR team, or HR team exists).
- **R2:** 2 families (payroll role, or HR generalist role).
- **Total:** 2 x 2 = 4 cells.

| Cell | Deterministic read | What it tells us (inferred situation) | The angle it earns | Contact 1, then contact 2 |
|---|---|---|---|---|
| **A. First HR hire** | R1 = 0, and R2 = generalist | Until now, people work has been done by someone outside HR, most likely the founder or an operations or finance person. The company is now hiring its first HR person to take it over. Payroll and remittances are probably part of that handover | Your first HR hire shouldn't inherit the spreadsheets. Put payroll, PAYE and pension on a system before they start, so they take over a process that already runs. Proof: Famasi, where the founder ran payroll and remittances by hand and now does it in under 5 minutes [fa] | CEO or founder. No second contact |
| **B. First payroll hire** | R1 = 0, and R2 = payroll | The company has outgrown having payroll run on the side and is adding a salary to do it. It's solving payroll by hiring a person | Before adding a person to run payroll and remittances, see them run automatically. The hire can then check payroll instead of building it every month. Proof: Famasi's under 5 minutes [fa] | CEO or founder. No second contact |
| **C. Growing the HR team** | R1 = 1+, and R2 = generalist | An HR function exists and is adding capacity or replacing someone. HR workload is rising with headcount | One platform for the work the new person will spend their days on: leave, loans, salary advances, expenses, records and reviews. The new hire starts in a system, not an inbox. Proof: Nikky Taurus (requests handled faster) and Kredete (came for payroll, used HRIS and OKRs too) [fa] | HR or People lead, then the CEO 3 days later (the Finance lead instead at 100+ staff) |
| **D. Payroll split out of HR** | R1 = 1+, and R2 = payroll | The HR team is moving payroll into a dedicated role. Payroll volume or complexity is now big enough for a specialist, at the moment the 2026 PAYE bands are live | The new payroll role should start on payroll already updated for the new tax law, with PAYE, pension, NHF and NSITF filed automatically. Proof: "₦934M in PAYE filed and ₦754M in pension processed in 2025, all on time" [fa] | HR or People lead, then the Finance lead (100+ staff) or the CEO |

### Branch coverage

- **All 4 cells:** the job title, company name, job board and posted date are available, so every angle can name the role being hired.
- **Cells A and B:** there's no HR person to name. The angle never refers to an HR lead.
- **Cells C and D:** an HR lead's name exists and can be used for contact 2.
- **"No HR team" can be wrong:** R1 = 0 is read from LinkedIn, which may miss people at Nigerian SMEs [sm]. So the A and B angles never state "you run payroll yourself" as a fact. They talk about what happens next (the hire takes over), and the Famasi story implies the rest.

### Niche-native test

- Each angle hangs on two facts that only this company has: the exact role they posted, and whether an HR team already exists.
- The proof in each cell (Famasi, Nikky Taurus, Kredete, the 2025 remittance record) is PaidHR-only and approved in facts.md.

### Context lines

These are allowed in any cell, and each adds at most one line. They never change the angle.

| Read | When it fires | What it may add |
|---|---|---|
| C1 remittance duty in the job description | Match is not `none` | Names the duty from their own post (for example pension remittances) as the work PaidHR automates |
| C2 annual return window | Sent 1 Dec to 31 Jan | The first annual return on the 2026 bands is due 31 January; PaidHR is updated for the new law. No penalty figures [fa] |
| C3 multi-state | Jobs in 2+ states | Approved line: handles multi-state payroll and remits taxes and pensions in different states [fa] |
| C4 funding | Raised in the last 12 months | Mentions the round as the reason headcount is growing. No amounts |
| C5 hiring fast | 5+ posts in 60 days | Says "hiring fast" only, never a count |

## 6. Variables contract [ENGINE]

| Variable | Source field | Exists in |
|---|---|---|
| `{{first_name}}` | Clay Find People: contact first name | All cells |
| `{{company_name}}` | Clay company lookup: name, cleaned of "Ltd", "Nig" and similar | All cells |
| `{{job_title}}` | Apify job post `title`, cleaned to title case | All cells |
| `{{job_board}}` | Apify source (Jobberman, MyJobMag, LinkedIn) | All cells |
| `{{cell}}` | Clay formula on R1 and R2: A, B, C or D | All cells (picks the template; never printed) |
| `{{contact_role}}` | Clay formula: CEO, HR lead or Finance lead | All cells (picks the template; never printed) |
| `{{hr_lead_first_name}}` | Clay Find People: first HR or People title | **C and D only** |
| `{{jd_duty}}` | C1 enum mapped to a phrase: `paye` = "PAYE schedules", `pension` = "pension remittances", `remittance` = "statutory remittances" | All cells, **only when C1 is not `none`** |
| `{{in_return_window}}` | C2 date check (true or false) | All cells (turns the C2 line on or off) |
| `{{states_list}}` | C3: distinct states across job posts, joined ("Lagos and Abuja") | All cells, **only when C3 = multi-state** |
| `{{funding_round}}` | Crunchbase via Clay: last round type | All cells, **only when C4 is true** |
| `{{hiring_fast}}` | C5 cluster (true when 5+ posts) | All cells (turns the C5 line on or off) |
| `{{first_line}}` | Clay AI column: one opening line from the job post and cell, using facts.md claims only [gs] step 9 | All cells |
| `{{sender_name}}`, `{{sender_title}}`, `{{sender_signature}}` | facts.md sender identity, **still open** | All cells; blocks sending until set |

**Never handed to copy:**
- headcount
- raw counts of posts, states or HR staff
- the PenCom match
- the rival tool named in the job description
- `size_unverified`
- funding amount

## 7. Cadence and channel [ENGINE]

| Field | Value |
|---|---|
| Periodicity | Always on. Weekly scrape and weekly send batches, from 1 Dec 2026 |
| Channel | Email and LinkedIn |
| Shape | 3 emails over about 10 days, plus a LinkedIn connect and 1 message (starting default, INFERRED) [gs] step 9 |
| Second contact | Cells C and D only, starting 3 days after contact 1 |
| Stop rules | Any reply stops the sequence for the whole account [gs] step 10 |
| LinkedIn | Waits until a LinkedIn sending tool is chosen. Email runs without it |
| Re-entry | No reply: back to the signal pool; can re-enter on a new post after 90 days [gs] step 10 |

---

## Definition of done

- [x] Mother intent: one sentence, signal-led, matched to the catalog
- [x] Inclusion: ICP box, trigger definition and who we contact, tagged [ICP]
- [x] Exclusion: who's out and why
- [x] Sources: trigger plus every enrichment
- [x] Signals table: every read deterministic, every role declared
- [x] Count clusters declared for R1, C3 and C5
- [x] Routing matrix with every angle filled in
- [x] Branch coverage checked per cell
- [x] Variables contract: every variable mapped to its source field
- [x] Engine and ICP markers on every section
- [x] Cadence and channel declared

## Blockers before the first send (from gtm-system.md)

1. Sender chosen (`{{sender_name}}` and the rest).
2. Clay, HubSpot, n8n and PlusVibe connected.
3. PaidHR's customer and open-deal list loaded into HubSpot for exclusion.
4. A week of scraping to measure real volume (unknown today [sm]).

## Next

`/campaign-copy` on this file. Its GATE 1 checks this status and the checklist above.

---

## Copy

Syntax: `{{variable}}` for spec variables, `{a|b}` for spintax on static lines only. Cells A to D are exhaustive (R1 x R2 covers every lead), so cell-routed lines have no fallback. Persona review and human test run 2026-11-11; Email 1 revised and re-approved.

### Email 1 (day 0, new thread). APPROVED 2026-11-11

**Subject:** `{payroll before the new hire|{{company_name}} + payroll|before your new hire starts}`

**Greeting:** `{{first_name}},`

**Line 1, the hiring signal (by cell)**
- + CELL A: {{company_name}} is hiring for the {{job_title}} role, which I think would be your first HR hire.
- + CELL B: {{company_name}} is hiring for the {{job_title}} role, and I couldn't find anyone else in HR on the team.
- + CELL C: You're hiring for the {{job_title}} role at {{company_name}}.
- + CELL D: {{company_name}} has the {{job_title}} role open on {{job_board}}.

**Line 2, the inferred situation (by cell)**
- + CELL A: If payroll and remittances run on spreadsheets and bank files today, that's probably what they'd be taking over.
- + CELL B: My guess is payroll has grown past something that can be done on the side, and this hire is how it comes off someone's plate.
- + CELL C: I imagine a lot of that role is leave requests, loans, salary advances and expense claims, the work that grows with every new joiner.
- + CELL D: My guess is payroll and remittances have grown big enough to need someone full time.

**Line 3, context (waterfall, first match wins)**
- + C2 IN WINDOW (1 Dec to 31 Jan): And they'd probably start close to 31 January, when the first annual return on the new PAYE bands is due.
- + C1 DUTY MATCHED: The post even lists {{jd_duty}} as part of the job.
- + C3 MULTI-STATE: With roles open in {{states_list}}, that's PAYE going to more than one state.
- + C4 FUNDED: After the {{funding_round}} round, headcount is probably still climbing.
- + C5 HIRING FAST: And with the team hiring fast, that workload keeps growing.
- FALLBACK: And since January, every payroll has had to run on the new PAYE bands.

**Line 4, value prop (static):** `{At PaidHR we run payroll|We run payroll at PaidHR} and file PAYE and pension automatically, already updated for Nigeria's new tax law.`

**Line 5, proof (by cell)**
- + CELL A: Famasi's CEO was running payroll and remittances by hand and cut it to under 5 minutes.
- + CELL B: That's how Famasi's CEO, who was doing it all by hand, got payroll and remittances to under 5 minutes.
- + CELL C: Nikky Taurus's HR & Admin Manager moved that work onto PaidHR and says turnaround on those requests has been "very impressive".
- + CELL D: In 2025 that came to ₦934M in PAYE filed and ₦754M in pension processed, all on time.

**CTA (static):** `{Worth setting up before the new hire starts?|Would it help to have this running before they start?|Worth a look before the new hire's first payroll?}`

**Sign-off (static):** `{Best,|Thanks,|Regards,}`

`{{sender_signature}}`

**Sample, cell A, December send:**

> payroll before the new hire
>
> {{first_name}},
>
> {{company_name}} is hiring for the HR Manager role, which I think would be your first HR hire.
>
> If payroll and remittances run on spreadsheets and bank files today, that's probably what they'd be taking over.
>
> And they'd probably start close to 31 January, when the first annual return on the new PAYE bands is due.
>
> At PaidHR we run payroll and file PAYE and pension automatically, already updated for Nigeria's new tax law.
>
> Famasi's CEO was running payroll and remittances by hand and cut it to under 5 minutes.
>
> Would it help to have this running before they start?
>
> Best,
> {{sender_signature}}

### Email 2 (day 3, reply in thread, subject "Re:"). APPROVED 2026-11-11

**Line 1, the next problem (by cell)**
- + CELL A: Once your first HR hire starts, payroll is probably only part of what they'll run.
- + CELL B: If the new {{job_title}} is going to check payroll rather than build it every month, you need to trust what's doing the filing.
- + CELL C: Of those requests, salary advances are probably the ones that pile up around month-end.
- + CELL D: If payroll moves onto a new system along with the new hire, your salary and tax data moves with it.

**Line 2, proof (by cell)**
- + CELL A: Kredete came to PaidHR for payroll and ended up managing employee records, OKRs and team activities on it too.
- + CELL B: In 2025 PaidHR filed ₦934M in PAYE and processed ₦754M in pension with zero statutory defaults or delays.
- + CELL C: With Earned Wage Access, staff draw pay they've already earned at no cost to your company, and you do not fund the advances.
- + CELL D: PaidHR is ISO 27001 certified and NDPA registered, with zero statutory defaults or delays.

**CTA (static):** `{Relevant for {{company_name}}?|Would that help at {{company_name}}?|Worth a look for {{company_name}}?}`

**Sign-off (static):** `{Best,|Thanks,|Regards,}` then `{{sender_signature}}`

### Email 3 (day 10, reply in thread). APPROVED 2026-11-11

**Line 1 (static):** `{Last note from me on this one.|I'll leave it here after this.|This is my last message on it.}`

**Line 2, the close (by cell)**
- + CELL A or B: Would it make more sense to pick this up once your new {{job_title}} has started?
- + CELL C or D: If payroll sits with someone else at {{company_name}}, who would be the right person to ask?

**Sign-off (static):** `{Best,|Thanks,|Regards,}` then `{{sender_signature}}`

### LinkedIn. APPROVED 2026-11-11

**Connection request:** no note.

**DM 1, after connecting (by cell)**
- + CELL A: {{first_name}}, is payroll moving over to the new {{job_title}} once they start, or staying with you?
- + CELL B: {{first_name}}, will the new {{job_title}} be setting payroll up from scratch, or taking over a system you already use?
- + CELL C: {{first_name}}, will the new {{job_title}} take on leave and salary advance requests, or is that staying with you?
- + CELL D: {{first_name}}, is the new {{job_title}} taking over PAYE and pension filing, or will that stay with HR?

**DM 2 (static, sent only if DM 1 gets no reply):** `Asking because I work at PaidHR, and that handover is pretty much what we do: we run payroll and file PAYE and pension automatically. {Happy to show you how it works if useful.|Can show you how it would look at {{company_name}} if useful.}`

No DM 3.
