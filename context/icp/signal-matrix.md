# PaidHR Signal Matrix

**Status: WORK IN PROGRESS (v0.1, 2026-11-10).** These are hypotheses to test with sales and the CRM, not decisions.

**Built from:**
- context/icp/icp.md and context/icp/personas.md
- context/docs/research/
- the method in knowledge-base/playbooks/signal-matrix-framework.md and workflow-anatomy.md

**Source tags:**

| Tag | File |
|---|---|
| [co] | company.md |
| [cu] | customers.md |
| [cp] | competitors.md |
| [mk] | market.md |
| [sg] | signals.md |
| [vo] | voice.md |
| [icp] | icp.md |
| [pe] | personas.md |
| [web] | data sources checked by web search on 2026-11-10 (links in Data source notes) |

**INFERRED** means the research doesn't state it; it's our reading. All scores are INFERRED. No signal has been tested against closed deals yet ([sg] Gaps).

**Product.** PaidHR sells one platform: HR, payroll, automatic PAYE and pension remittance, employee finance (EWA, Loan Marketplace) and Cross Border by PaidHR [co]. Each cell gets a lead pillar from context/messaging/messaging.md, not a separate product.

---

## Matrix 1: Segments x personas

### Why these rows

Firmographics only narrow the market to "Nigerian employer, 20+ staff" [icp]. Rows are therefore split by **situation**: the observable fact that changes urgency and angle. Every row inherits two hard filters: payroll run in Nigeria, and 20+ employees [icp].

Rows overlap, so each company goes in the **first row it matches**, top to bottom. That keeps every company in exactly one cell.

| # | Segment | Target definition (Clay-filterable) | Evidence |
|---|---|---|---|
| S1 | Recent switchers | Known users of Bento Africa (collapsed Feb 2025) or a named rival (SeamlessHR, Workpay, PayDayNG) | [cp], [sg] Provider failure |
| S2 | Funded startups | Nigeria HQ, raised seed to Series B in the last 12 months, 20 to 200 staff on LinkedIn | [sg] Funding (Famasi) |
| S3 | Multi-location or cross-border | Job posts or offices in 2+ Nigerian states, OR staff or contractors in another country. Excludes foreign firms needing a legal Employer of Record (not a fit [icp]) | [co] Modules, [sg] Expansion |
| S4 | Frontline-heavy | 50+ staff, and most open roles are hourly or field roles (drivers, riders, cashiers, sales reps, nurses, guards) | [sg] Retention, [co] Time & Attendance. Sector fit INFERRED |
| S5 | HR-led SME | 20 to 200 staff, at least one HR / People title on LinkedIn, none of the triggers above | [cu] Kredete, Nikky Taurus |
| S6 | Owner-run SME | 20 to 50 staff, no HR, People or Finance title on LinkedIn (founder runs payroll) | [cu] Famasi |

**Company examples:** not filled in. Each cell needs a Clay research run with the filters above. No names were invented. The named customers (Famasi, Kredete and others) are reference accounts for lookalikes (signal N8), not targets.

**Partner channel** (payroll consultants and agencies [sg]): left out. It's a different motion, with a different buyer and a different offer.

### Angle per cell

Columns follow personas.md:
- **Champion:** HR / People lead.
- **Economic buyer:** CEO or founder. In firms of 100+, Finance may sign instead (INFERRED [pe]).
- **Influencer:** Finance or payroll admin.

| Segment | Champion (HR / People lead) | Economic buyer (CEO / founder) | Influencer (Finance / payroll admin) |
|---|---|---|---|
| S1 Recent switchers | Remittances you can see confirmed, plus a team that helps with onboarding (Bova Media onboarding quote [cu]). Never name Bento or a rival [facts.md] | Trust: 2025 PAYE and pension filed on time, ISO 27001 and NDPA, backed by Accion [co] | Clean migration: journals into the ERP, PAYE and pension schedules from day one [co]. INFERRED |
| S2 Funded startups | You're about to hire fast: one record from offer to payslip (PaidHiring plus payroll) [co] | Stop running payroll yourself as headcount grows; Famasi's CEO got it to under 5 minutes [cu] | Board-ready payroll: tax bands, pension and journals right from the first big hiring wave. INFERRED |
| S3 Multi-location / cross-border | One run for every state, with each state's taxes and pensions remitted [sg] Expansion | Pay staff in other countries without opening a local office (CEO quote) [sg] | Multi-state remittance and foreign-currency pay in one ledger [co]. INFERRED framing |
| S4 Frontline-heavy | Hours tracked, hours paid (Time & Attendance) and fewer salary-advance requests [co], [cu] Nikky Taurus | Retention you don't have to buy: EWA costs the company nothing [vo], [co] | EWA advances not funded by the company; attendance feeds payroll [co] |
| S5 HR-led SME | Fewer chases: leave, loans, advances and expenses handled in one place [cu] Nikky Taurus; came for payroll, got HRIS and OKRs (Kredete) [cu] | New tax law already handled; no penalty exposure on the 2026 bands [co], [mk] | 2026 PAYE bands applied correctly; annual return due 31 January [mk] |
| S6 Owner-run SME | No HR lead here. The CEO is both champion and buyer: use the buyer column | Famasi story: payroll, PAYE and pension done "in less than 5minutes" [cu] | Often an outside accountant (INFERRED). Low priority |

### Segment assessment (Phase 2, all INFERRED)

| Segment | Signal density | Product fit | Reachability | Priority | Why |
|---|---|---|---|---|---|
| S5 HR-led SME | High | High | Med | **High** | Biggest pool. Hiring and new-leader signals fire here, and two of the three employer testimonials fit it [cu] |
| S6 Owner-run SME | Med | High | Med | **High** | Famasi is the only proof with a number [cu]. Signal: the first HR hire. Weak spot: small firms have little LinkedIn data |
| S4 Frontline-heavy | High | Med | Med | **Med-High** | Job boards show volume hiring well. The EWA fit is product-led; no frontline customer has been proven [icp] |
| S2 Funded startups | Med | High | High | **Med** | Clean data and a clean reason, but low volume (see U5) |
| S3 Multi-location / cross-border | Med | Med | Med | **Med** | Product claims support it, with no customer proof [icp] |
| S1 Recent switchers | Low | High | Low | **Low** | Bento collapsed 21 months ago, so most of its customers have probably moved already (INFERRED). Rival users can't be detected well |

---

## Matrix 2: Signals

Four tests from workflow-anatomy.md, each scored 1 to 5 (all INFERRED):
- **R:** a clear buying reason
- **V:** enough volume
- **D:** data you can get
- **S:** a natural story

Total is out of 20.

**Type:**
- **U = Universal:** the same build serves several segments; only keywords change.
- **N = Niche:** a source used for only one segment.

| ID | Type | Signal | Mother intent | Data source | Tool to detect it | Segments | R | V | D | S | Total | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| U1 | U | Job post for HR Manager, Payroll Officer, HR Generalist or HR & Admin Officer, Nigeria, last 30 days | Hiring specific roles | Jobberman, MyJobMag, LinkedIn Jobs (Nigeria) | Apify Jobberman actor, then Clay import; Clay "Find Jobs at Company" | S5, S6 (first HR hire), S4 | 4 | 4 | 4 | 5 | **17** | VERIFIED [web] |
| U2 | U | 5+ open roles in 60 days | Hypergrowth (hiring velocity) | Same scrape as U1, counted per company | Clay aggregation on the U1 table | S2, S4, S5 | 3 | 3 | 4 | 4 | 14 | VERIFIED [web] |
| U3 | U | New HR, People, Finance or CFO hire, start date under 90 days | New leadership | LinkedIn profiles | Clay "Find People" filtered by title and start date; Apollo | S5, S2, S3 | 4 | 3 | 3 | 5 | 15 | VERIFIED. Coverage of Nigerian non-tech firms on LinkedIn is INFERRED as weaker |
| U4 | U | Headcount up 20%+ in 6 months, or crossing 20 | Hypergrowth (headcount) | LinkedIn company headcount | Clay "Enrich Company" with monthly snapshots | S2, S5, S6 | 3 | 3 | 2 | 3 | 11 | VERIFIED (PARTIAL): LinkedIn headcount likely undercounts frontline staff (INFERRED) |
| U5 | U | Raised seed to Series B, Nigeria HQ, last 90 days | Fundraising | Crunchbase; funding roundups from Nairametrics, Launch Base, TechCabal | Clay "Find Organization" (Crunchbase); RSS feed via Clay HTTP | S2 only | 4 | 2 | 4 | 4 | 14 | VERIFIED [web]. Volume: 77 Nigerian startups raised $100k+ in Jan to Sep 2026, about 9 a month [web] |
| U6 | U | Annual return due 31 January, first full year under the new PAYE bands | Regulatory changes | DLA Piper NTA FAQ [mk], [sg] | None needed: a calendar window (Dec to Jan) laid over U1 to U5 | All | 4 | 5 | 5 | 5 | 19 | VERIFIED (COMPOUND): timing only, never a list on its own. "First full year" is INFERRED from the 1 Jan 2026 start date |
| U7 | U | Engaged with LinkedIn posts on NTA payroll changes | LinkedIn content engagement | Posts by Nigerian tax advisers and HR voices | Apify LinkedIn post-reactions actor, then Clay | S5, S6 | 3 | 3 | 3 | 4 | 13 | VERIFIED (PARTIAL): actor not checked; INFERRED |
| N1 | N | Job posts in 2+ Nigerian states, or a new branch | Niche-specific (expansion) | Location field on Jobberman posts; Google Maps place count | Apify Jobberman (location field [web]); Google Places API via Clay HTTP | S3 | 3 | 3 | 4 | 4 | 14 | VERIFIED [web] |
| N2 | N | Nigerian firm hiring in Kenya, Ghana or South Africa, or paying contractors abroad | Hiring offshore | Jobberman, BrighterMonday, Careers24 | Apify "Africa Jobs Scraper" [web] | S3 | 3 | 2 | 3 | 4 | 12 | VERIFIED [web]. Excludes Employer of Record needs [icp] |
| N3 | N | 10+ posts in 60 days for drivers, riders, cashiers, sales reps, nurses or guards | Hiring specific roles (frontline keywords) | Same scrape as U1, different keywords | Apify Jobberman, then Clay | S4 | 3 | 4 | 4 | 4 | 15 | VERIFIED [web]. Sector fit INFERRED |
| N4 | N | Employer on PenCom's list of uncredited or defaulted remittances | Regulatory changes | pencom.gov.ng "list of employers" section [web] | crawl4ai or Clay HTTP scrape, matched to company records | S5, S6 | 5 | 2 | 3 | 1 | 11 | VERIFIED (PARTIAL): page format not checked. **Use for routing and priority only. Never mention it in copy** (facts.md bans diagnosing failure) |
| N5 | N | Ex-Bento Africa customer | Competitor customers | Bento's archived logo and case-study pages on the Wayback Machine | crawl4ai on archived pages | S1 | 2 | 2 | 2 | 2 | 8 | PARTIAL: a one-off list build, not a workflow |
| N6 | N | Job post naming SeamlessHR, Workpay or PayDayNG as a required skill | Competitor customers | Job descriptions from the U1 scrape | Keyword filter in Clay | S1 | 2 | 2 | 3 | 2 | 9 | PARTIAL. INFERRED |
| N7 | N | Sponsor or exhibitor at CIPM ICE (Africa's largest HR event; 58th edition 21 to 24 Sep 2026, Abuja) | Event sponsorship | cipmnigeria.org | Clay HTTP or manual scrape of the sponsor page | S5 | 2 | 2 | 2 | 3 | 9 | PARTIAL: attendee list isn't public. Next edition expected about Sep 2027 (INFERRED) |
| N8 | N | Lookalikes of named customers (Famasi, Kredete, Jamit, Bova Media, Nikky Taurus) | Customer lookalikes | The customers' own domains | Clay lookalike or Ocean.io | S2, S5, S6 | 2 | 4 | 3 | 3 | 12 | PARTIAL: needs the CRM customer list. Naming customers in copy needs approval (facts.md) |
| N9 | N | Past PaidHR admin users who moved to a new company | Champion migration | CRM export | Clay people enrichment (job change) | All | 5 | ? | ? | 5 | n/a | BLOCKED: needs CRM data. Likely the strongest signal once it's available (INFERRED) |

### Killed

| Signal | Why |
|---|---|
| Website visitors (RB2B) | Person-level identification works only for US companies (workflow-anatomy.md) |
| BuiltWith technographics | Payroll software runs in the back office and can't be seen on a website (framework) |
| Funding for S3 to S6 | Most of these are not VC-backed (INFERRED). U5 is kept for S2 only |
| Blog RSS content intent | Prospects' blog URLs aren't known in advance, so it's not worth building |

### Signals by segment

| Segment | Signals |
|---|---|
| S1 | N5, N6 (all weak) |
| S2 | U5, U2, U3, U4, N8 |
| S3 | N1, N2, U3 |
| S4 | N3, U2, U1 |
| S5 | U1, U3, U2, U7, N4, N7, N8 |
| S6 | U1 (first HR hire), U4, U7, N4, N8 |
| All | U6 timing window; N9 once the CRM is available |

**What builds once and serves many:**
- **One Jobberman scrape** feeds U1, U2, N1, N3 and N6: five signals from one Clay build, with only keyword and location filters changing.
- **Universal signals:** 7 of the 15 scored signals.

---

## Build first

| Rank | Signal | Why |
|---|---|---|
| 1 | **U1 HR / payroll hiring** (17/20) | The highest score among the list-building signals. Scraping costs about $1 per 1,000 results on Apify [web]. It serves the two High-priority segments (S5, S6), and the story is natural: a new HR hire inherits payroll and the new tax rules |
| 2 | **U6 annual return window** (19/20, compound) | Not a list, but a deadline: returns are due 31 January 2027 for the first full year on the new PAYE bands [mk]. Apply it to U1 and U3 and start sending in early December. Without it the best timing passes for another year |
| 3 | **U3 new HR / Finance leader** (15/20) | Matches the only evidence of how PaidHR gets adopted: a leader brings in a new tool (Kredete [cu]). Reuses Clay "Find People" |
| 4 | **N3 frontline volume hiring** (15/20) | Same Jobberman build as U1, so it costs almost nothing extra. It opens the EWA pillar, the one angle competitors can't match on cost [co]. Sector fit is INFERRED, so test it as a small batch |
| 5 | **U5 funding** (14/20) | Clean data and a clear reason for S2. Low volume (about 9 a month [web]), so keep it as a steady side workflow, not the main engine |

N9 (champion migration) goes to the top as soon as CRM data is available.

---

## Matrix 3: Workflow tracker

Every row starts as "Planned". The other columns from the framework (Campaigns, Launch date, Persona, Clay URL, metrics and the rest) fill in at launch.

| W # | Status | Workflow name | Mother intent | Segments |
|---|---|---|---|---|
| W1 | Planned | HR and payroll hiring, Nigeria | Hiring specific roles | S5, S6, S4 |
| W2 | Planned | Annual return window (Dec to Jan overlay) | Regulatory changes | All |
| W3 | Planned | New HR / Finance leader, 90 days | New leadership | S5, S2, S3 |
| W4 | Planned | Frontline volume hiring | Hiring specific roles | S4 |
| W5 | Planned | Fresh funding, Nigeria | Fundraising | S2 |
| W6 | Planned | Hiring velocity | Hypergrowth (hiring) | S2, S4, S5 |
| W7 | Planned | Multi-state expansion | Niche-specific (expansion) | S3 |
| W8 | Planned | Cross-border hiring | Hiring offshore | S3 |
| W9 | Planned | Headcount growth | Hypergrowth (headcount) | S2, S5, S6 |
| W10 | Planned | NTA post engagers | LinkedIn content engagement | S5, S6 |
| W11 | Planned | Customer lookalikes | Customer lookalikes | S2, S5, S6 |
| W12 | Planned | PenCom list routing (priority flag only) | Regulatory changes | S5, S6 |
| W13 | Planned | CIPM ICE sponsors | Event sponsorship | S5 |
| W14 | Planned | Competitor-tool job posts | Competitor customers | S1 |
| W15 | Planned | Ex-Bento list (one-off) | Competitor customers | S1 |
| W16 | Blocked | Champion migration | Champion migration | All |

---

## Data source notes (checked 2026-11-10)

- **Jobberman scrapers:** several Apify actors exist, priced from about $1 per 1,000 results, returning location, company and posted-date fields. An Africa-wide actor covers Jobberman, MyJobMag, BrighterMonday and Careers24.
  - https://apify.com/blackfalcondata/jobberman-scraper
  - https://apify.com/unfenced-group/jobberman-com-scraper
  - https://apify.com/jungle_synthesizer/africa-jobs-aggregator-scraper
- **PenCom list:** PenCom posts a "list of employers" with uncredited remittances on pencom.gov.ng, and recovered ₦2.06bn from 49 defaulting employers in Q3 2025.
  - https://www.mondaq.com/nigeria/retirement-superannuation-pensions/1371524/pencom-directive
  - https://allafrica.com/stories/202512100217.html
- **Nigerian funding volume:** 77 Nigerian startups raised at least $100k in Jan to Sep 2026 (Africa: The Big Deal, as summarised in search results; primary report not opened). Monthly deal counts from Nairametrics.
  - https://nairametrics.com/2026/07/16/nigerian-startups-top-10-attract-132-2-million-capture-71-funding-in-h1-2026/
- **CIPM ICE 2026:** 21 to 24 Sep 2026, Abuja, 4,000+ delegates.
  - https://cipmnigeria.org/cipm-announces-theme-dates-and-opens-registration-for-the-58th-international-conference-and-exhibition-africas-largest-hr-event/
  - https://guardian.ng/?p=2923025

## Open questions

- Actual monthly volume for U1 and N3: run the scraper for 30 days and count before trusting the V scores.
- How well LinkedIn covers Nigerian SMEs (affects U3, U4, S6).
- CRM: closed-won industries, sizes and signals; past users for N9; the customer list for N8.
- Format of the PenCom list page and how often it's updated.
- Google Sheets push skipped: no WORKFLOW_TRACKER_SPREADSHEET_ID in .env.
