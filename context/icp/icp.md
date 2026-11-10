# PaidHR ICP

Built only from `context/docs/research/` (checked 2026-11-09). Source tags: **[co]** company.md, **[cu]** customers.md, **[cp]** competitors.md, **[mk]** market.md, **[sg]** signals.md, **[vo]** voice.md. `INFERRED` = our reading of the research, not a stated fact.

## 1. Firmographic

The evidence supports only two hard filters, so firmographics alone give a broad list ("Nigerian employer, 20+ staff"). Layers 2 and 3 do the narrowing.

**Hard filters (use to build the list)**

| Filter | Why | Source |
|---|---|---|
| Runs payroll in Nigeria | Statutory remittance evidence is Nigeria only (PAYE, pension, NHF, NSITF). Every named customer with a known country is Nigerian | [co] Modules, [cu] Named customers |
| 20+ employees | Lowest published tier is "20 - 100 Employees" | [co] Pricing |

**Ranking boosts (product fit, no customer proof yet)**

| Boost | Why | Source |
|---|---|---|
| Staff in more than one Nigerian state | Payroll page claims multi-state tax and pension remittance | [co] Modules |
| Shift or field staff | Time & Attendance module | [co] Modules |
| Staff or contractors paid in other currencies | Cross Border by PaidHR | [co], [sg] Expansion |

**Claimed, not proven: do not target on these yet**

| Claim | Problem | Source |
|---|---|---|
| Industries: "logistics, retail, manufacturing, and financial services" | Comes from seed-round press (Launch Base; Nairametrics says "banking"), so it is PaidHR's pitch. Named customers are pharmacy (Famasi), shipping (Heroshe), media and fintech (INFERRED) and a non-profit; none in retail or manufacturing. No vertical focus shown (INFERRED) | [cu] Industries, Named customers |
| Kenya, Ghana, South Africa | CEO claim only; Launch Base omits Ghana; no customers there found | [co] Markets, Gaps |
| 100+ employees / "enterprise" | Enterprise tier exists ("Everything in Standard + Dedicated support"), but no named customer's headcount was found | [co] Pricing, [cu] Company sizes |

Removed: the "average customer about 60 employees" estimate (built from homepage counts that conflict, see facts.md), the low-wage workforce statistic (true of the whole market, so it filters nothing) and the "growing SMEs to mid-market" stage line (no evidence behind it).

## 2. Technographic

| Today's setup | What it tells us | Source |
|---|---|---|
| Spreadsheets plus bank bulk-upload files | Core displacement target | [cp] Non-software alternatives, [vo] |
| Founder or HR doing remittances by hand | Highest-pain setup (Famasi before PaidHR) | [cu] Testimonials |
| Several disconnected HR, payroll, attendance tools | Target of "People operations without the patchwork" | [vo] Homepage headlines |
| ERP / finance systems in place | Fits Enterprise pitch (payroll journals pushed to ERP) | [co] Modules (Integrations) |
| Former Bento Africa customer | Switching pool after Feb 2025 collapse | [cp] Bento Africa |
| Incumbent: SeamlessHR, Workpay, PayDayNG, Zoho People, SAP SuccessFactors | Competitive displacement, harder | [cp] |
| Payroll config not yet updated for NTA 2025 bands | Compliance exposure | [mk] Digital enforcement |

## 3. Intent signals

Ranked by urgency (INFERRED ranking). Full evidence in [sg].

| Signal | Why now | Source |
|---|---|---|
| NTA 2025 payroll changes (live 1 Jan 2026), annual returns due 31 January | 40% penalty for failure to deduct, 10% plus interest for failure to remit, managers pursuable | [mk], [sg] |
| PenCom / state IRS enforcement on the company or its sector | Recovery drives (₦36.6bn recovered) | [mk] Pensions |
| Payroll provider failure (Bento) | Needs a new provider now | [sg] Provider failure |
| New HR, People or Finance leader | New leaders bring tools (Kredete) | [sg] New leaders |
| Crossing 20 employees / hiring several roles | Enters lowest tier; hiring volume | [sg] Hiring |
| Fresh funding round | Headcount growth follows (INFERRED) | [sg] Funding |
| New state or country, foreign-currency staff | Cross-border and multi-state payroll | [sg] Expansion |
| High turnover / many salary-advance requests | EWA and Loan Marketplace angle | [sg] Retention |

## 4. Persona (summary, detail in personas.md)

| Role | Who | Source |
|---|---|---|
| Champion | Head of People / HR & Admin Manager | [cu] Kredete, Nikky Taurus testimonials |
| Economic buyer | CEO / founder (SME); Finance lead in larger firms (INFERRED) | [cu] Famasi, Kredete ("our CEO introduced Pade") |
| Influencer | Finance / payroll admin; employees (can "Refer your Employer") | [co] Modules, [vo] Loan Marketplace page |

## 5. Engagement readiness

INFERRED tiers, built from [sg]. Not yet validated against deals.

| Tier | Condition | Action |
|---|---|---|
| Ready now | Compliance trigger or provider failure, AND payroll still manual or on old setup | Lead with compliance pillar |
| Warm | Growth trigger (funding, hiring, new leader, new state/country) | Lead with time saved / one platform |
| Nurture | Fits firmographics, no trigger seen | Content: tax law guide, PaidRight salary report ([co], [mk]) |

## Not a fit

| Who | Why | Source |
|---|---|---|
| Under 20 employees | Below the lowest published tier ("20 - 100 Employees") | [co] Pricing |
| Foreign firm needing a legal Employer of Record in Nigeria | No EOR product found for PaidHR; Workpay and Deel sell EOR | [cp] Workpay, Deel |
| Payroll run mainly outside Nigeria needing local statutory filing there | Statutory remittance evidence is Nigeria-only (PAYE, pension, NHF, NSITF) | [co] Modules |
| Buyer wanting a free tool only | Free options exist (LeadstackHR); PaidHR is paid, prices unpublished | [cp] Others |

## Open questions

- Upper size limit: homepage says "African enterprises"; Xceed365HR owns 500+. Does PaidHR win at 500+? [co], [cp]
- Kenya / Ghana / South Africa: customer counts and local compliance support not found. [co] Gaps
- Which signals actually came before closed deals: needs CRM data. [sg] Gaps
- Best-fit industry and headcount band: needs closed-won data from the CRM (industry, employees, deal size, win rate). Until then the industry and size claims above stay unproven. [cu] Company sizes
