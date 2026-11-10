# PaidHR Campaign Strategy

**Status:** v0.1, 2026-11-10. Ideas to choose from, not approved workflows. Pick one, then run `/build-workflow-spec` on it.

**Built from:**
- CLAUDE.md
- context/icp/ (icp.md, personas.md, signal-matrix.md)
- context/positioning/
- context/messaging/ (messaging.md, facts.md)
- context/docs/ (case-studies.md, gtm-system.md, research/)
- knowledge-base/playbooks/workflow-anatomy.md (Mother Intent Catalog)

meetings/ and knowledge-base/learnings/ are empty, so nothing here comes from sales calls or past campaigns.

**Source tags:**

| Tag | File |
|---|---|
| [co] | research/company.md |
| [cu] | research/customers.md |
| [cp] | research/competitors.md |
| [mk] | research/market.md |
| [sg] | research/signals.md |
| [sm] | context/icp/signal-matrix.md |
| [fa] | context/messaging/facts.md |

`INFERRED` means our reading, not a stated fact. Every score and ranking below is INFERRED, because no signal has been tested against closed deals yet ([sg] Gaps).

---

## Summary

- **Target audience (given):** Nigerian employers with 20+ staff that run payroll in Nigeria [icp]. The six segments S1 to S6 come from signal-matrix.md.
- **What PaidHR sells:** one platform for payroll, automatic PAYE, pension, NHF and NSITF remittance, HR tools, and earned wage access (EWA) at no cost to the employer [co].
- **Differentiators:** published 2025 remittance record, EWA the employer does not fund, updated for the Nigeria Tax Act 2025, multi-state remittance [co], [fa].

---

## Customer discovery analysis

| Customer | Industry | Size | Key metric | Problem solved | Usable in copy |
|---|---|---|---|---|---|
| Famasi | Digital pharmacy, founded 2021 | Not found | Payroll and remittances "in less than 5minutes", "at least 3hours" saved | CEO ran payroll and remittances by hand | Yes [fa] |
| Kredete Inc | Fintech (INFERRED) | Not found | None | Bought for payroll, then used HRIS and OKRs too | Yes, quote only [fa] |
| Nikky Taurus Nig LTD | Not found | Not found | None | Slow leave, loan, advance and expense handling | Yes, quote only [fa] |
| Jamit Technologies | Not found | Not found | None | Ease of use, support | No (not approved) |
| Bova Media | Media (INFERRED) | Not found | None | Fast payroll, onboarding | No (not approved) |
| Heroshe | Shipping | Not found | None | Not found | No (possible shutdown) [fa] |

Source: context/docs/case-studies.md.

**Patterns:**
- **Industries:** health, fintech, media and a non-profit, with no clear vertical [cu]. The "logistics, retail, manufacturing, financial services" list is seed-round press, not proof [icp].
- **Sizes:** unknown for every customer [cu].
- **Who bought:** the CEO (Famasi); the CEO introduced it and HR adopted it (Kredete); an HR & Admin Manager (Nikky Taurus) [cu].
- **Common problems:** the founder running payroll and remittances by hand; HR chasing requests; a tool that only covered payroll [cu].

**Challenge to the targeting:**
- Two of three buyer stories start with a leader choosing the tool (Famasi, Kredete). Campaigns built on a person (a new leader, or a founder still doing payroll) are better supported than industry campaigns.
- PaidHR's site markets a Payroll API and Whitelabel to "consultants and agencies" [co]. That's a second audience outside the ICP, and idea 12 uses it.

**Best lookalike seeds:** Famasi first (the only story with a metric), then Kredete and Nikky Taurus. Lookalikes are weak until we have the CRM's closed-won list (see idea 16).

---

## How ideas are ranked

Ideas are sorted by **signal strength (R)** plus **data ease (D)**, each scored 1 to 5. A tie goes to the higher Tier. Scores reuse signal-matrix.md where the signal is there; new ones are marked INFERRED.

**Volume:**
- Only one figure has a source: funding, at about 9 Nigerian rounds a month [sm].
- Every other volume is **unknown**. It shows as High, Med or Low (INFERRED) and needs a 30-day count before you trust it (signal-matrix.md open question).

**Difficulty:**
- **Low:** one scrape or one Clay enrichment.
- **Med:** two or more sources, or AI research per row.
- **High:** manual work, a one-off build, or data we don't have.

---

## Campaign ideas, ranked

| # | Campaign | Level | Mother intent | Segment and persona | Signal and data source | Angle | Volume a month | Difficulty | R+D | Tier |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | **January returns countdown** | Broad (timing overlay) | Regulatory changes | All segments; HR lead, or CEO in S6 | Annual return due 31 Jan, first full year on the new PAYE bands. Source: DLA Piper [mk]. Calendar window, Dec to Jan | Your first annual return on the 2026 bands is due 31 January; PaidHR is already updated for the new law | Not a list. Sized by whatever list it runs on | Low | 4+5=9 | Tier 1: deadline is fixed and public; window opens in about 3 weeks |
| 2 | **HR and payroll hire** | Focused | Hiring specific roles | S5 HR-led SME; HR lead (new hire's manager), CEO | Job post for HR Manager, Payroll Officer, HR Generalist or HR & Admin Officer, Nigeria, last 30 days. Jobberman, MyJobMag, LinkedIn Jobs via Apify [sm] | You're hiring someone to run HR and payroll; give them a system that already files PAYE and pension on time | Unknown. High (INFERRED) | Low | 4+4=8 | Tier 1: score 17/20 [sm], cheap scrape, one build serves 5 signals |
| 3 | **Remittance in the job description** (stretch) | Niche | Hiring specific roles | S5, S6; CEO or Finance lead | Same scrape as #2; AI reads the job description for "PAYE", "pension schedule", "remittance", "Excel", "bank upload" | The role you're hiring for spends its week on remittance schedules; PaidHR files them automatically | Unknown. Subset of #2 (INFERRED Med) | Low (one AI column on #2) | 4+4=8 | Tier 1: no extra source, sharper hook than #2 |
| 4 | **Fresh funding** | Focused | Companies fundraising | S2 Funded startups; CEO / founder | Seed to Series B, Nigeria HQ, last 90 days. Crunchbase via Clay; Nairametrics, Launch Base, TechCabal roundups [sm] | You're about to hire fast; Famasi's CEO cut payroll and remittances to under 5 minutes | About 9 rounds a month [sm] | Low | 4+4=8 | Tier 2: clean signal, low volume |
| 5 | **First HR hire at an owner-run SME** (Golden ICP) | Niche | Hiring specific roles | S6 Owner-run SME, 20 to 50 staff, no HR or Finance title on LinkedIn; CEO | #2 scrape, filtered to companies where Clay "Find People" returns no HR, People or Finance title | You've been running payroll yourself; before your first HR hire starts, hand both of you a system. Famasi story | Unknown. Med (INFERRED) | Med (people check per company) | 4+3=7 | Tier 1: closest match to the only proof with a number (Famasi) |
| 6 | **New HR or People leader** (New Hire) | Focused | New leadership (90 days) | S5, S2, S3; new Head of People, HR Manager | Start date under 90 days in an HR or People title. Clay "Find People", Apollo [sm] | First 90 days: inherit payroll on the new tax bands without inheriting the spreadsheets. Kredete: came for payroll, got HRIS and OKRs | Unknown. Med (INFERRED); Nigerian LinkedIn coverage may be thin [sm] | Med | 4+3=7 | Tier 1: matches how Kredete adopted it [cu] |
| 7 | **New Finance lead or CFO** | Focused | New leadership (90 days) | S2, S3, firms of 100+; CFO / Finance lead | Start date under 90 days in a Finance title. Clay "Find People" [sm] | Correct deductions on the 2026 bands, remittances confirmed, journals into the ERP | Unknown. Low to Med (INFERRED) | Med | 4+3=7 | Tier 2: no finance-buyer proof exists [fa] |
| 8 | **Frontline volume hiring, EWA** | Focused | Hiring specific roles (frontline keywords) | S4 Frontline-heavy, 50+ staff; HR lead, CEO | 10+ posts in 60 days for drivers, riders, cashiers, sales reps, nurses or guards. Same Jobberman scrape [sm] | Retention you don't have to buy: earned wage access at no cost to your company, and you don't fund the advances | Unknown. High (INFERRED) | Low | 3+4=7 | Tier 2: almost free to add to #2, but no frontline customer proven [icp] |
| 9 | **Hiring velocity** | Focused | Hypergrowth (hiring velocity) | S2, S4, S5; CEO, HR lead | 5+ open roles in 60 days, counted per company on the #2 scrape [sm] | Headcount is moving fast; one record from offer to payslip (PaidHiring plus payroll) | Unknown. Med (INFERRED) | Low | 3+4=7 | Tier 2: weaker reason than an HR-specific post |
| 10 | **Multi-state hiring** | Niche | Niche-specific play (expansion) | S3 Multi-location; HR lead, Finance | Job posts in 2+ Nigerian states, from the location field on the #2 scrape [sm] | One payroll run for every state, with each state's taxes and pensions remitted | Unknown. Med (INFERRED) | Low | 3+4=7 | Tier 2: product claim with no customer proof [icp] |
| 11 | **Branch count** (stretch, quantify the pain) | Niche | Niche-specific play (expansion) | S3 and S4: pharmacy, clinic, retail and fuel chains (INFERRED sectors); CEO, HR lead | Google Places count of a brand's branches and which states they're in, via Clay HTTP [sm] N1 | "You run {{branch_count}} branches across {{state_count}} states; each state's PAYE goes to a different tax office" | Unknown. Low to Med (INFERRED) | Med (place matching is messy) | 3+4=7 | Tier 2: strong personal hook, needs a match-quality check |
| 12 | **Payroll and accounting firms** (Creative, non-ICP) | Focused | Niche-specific play (partner channel) | Outside the ICP: Nigerian accounting firms, payroll bureaus and HR consultancies that run payroll for SME clients; Managing Partner | Google Maps categories ("accounting firm", "payroll services", "HR consulting") in Lagos and Abuja; firms' own service pages mention payroll or remittance (AI check) | Run your clients' payroll on PaidHR's infrastructure under your own name (Payroll API and Whitelabel) [co] | Unknown. Med (INFERRED) | Med | 3+4=7 | Tier 2: different offer and buyer; Whitelabel is "Request Early Access" [co], so confirm with Product before sending |
| 13 | **Creative ideas from their website** (Creative Ideas) | Broad | Niche-specific play | S5 base list; HR lead | AI reads the careers page, locations page and about page, and writes 3 ways PaidHR fits (for example shift staff to Time & Attendance, branches to multi-state, a benefits page to EWA) | "I had a few ideas for {{company}}" plus three bullets, each tied to one product module | Unknown. High, any base list (INFERRED) | Med (AI per row, prompt QA) | 2+4=6 | Tier 2: works on any list, but no trigger, so weak urgency |
| 14 | **NTA post engagers** | Focused | LinkedIn content engagement | S5, S6; HR lead, CEO, Finance | People who reacted to or commented on LinkedIn posts about NTA payroll changes by Nigerian tax advisers and HR voices. Apify post-reactions actor [sm] | You've been reading up on the new PAYE rules; PaidHR is already updated for them | Unknown. Med (INFERRED) | Med (actor not yet checked) | 3+3=6 | Tier 2: engagement is a soft signal |
| 15 | **Cross-border hiring** | Niche | Hiring offshore | S3; CEO, Finance lead | Nigerian firm posting jobs in Kenya, Ghana or South Africa. Apify Africa Jobs Scraper [sm] N2 | Pay staff in other countries without opening a local office (CEO quote [sg]) | Unknown. Low (INFERRED) | Med | 3+3=6 | Tier 3: excludes Employer of Record needs; cross-border claims aren't in facts.md yet |
| 16 | **Famasi lookalikes** (Lookalike) | Focused | Lookalike of customers | S2, S6: young Nigerian consumer health, pharmacy and e-commerce startups (INFERRED match to Famasi); CEO | Clay lookalike or Ocean.io seeded with famasi.africa (and Kredete); full seed list needs the CRM [sm] N8 | Famasi's CEO used to run payroll and remittances by hand; now it takes under 5 minutes | Unknown. Med (INFERRED) | Med | 2+3=5 (rises once the CRM list exists) | Tier 2: only 3 approved names; stronger once closed-won data arrives |
| 17 | **Headcount crossing 20, or up 20%** | Focused | Hypergrowth (headcount) | S2, S5, S6; CEO | LinkedIn headcount snapshots via Clay "Enrich Company", monthly [sm] U4 | You've just moved past 20 people, the point where payroll by hand starts to cost a founder real time | Unknown. Low (INFERRED) | Med (needs monthly snapshots) | 3+2=5 | Tier 3: LinkedIn undercounts frontline staff [sm] |
| 18 | **Rival tool in the job post** | Niche | Competitor customers | S1 Switchers; HR lead | Job descriptions from #2 that name SeamlessHR, Workpay or PayDayNG as a skill [sm] N6 | Remittances you can see confirmed (never name the rival [fa]) | Unknown. Low (INFERRED) | Low (keyword filter on #2) | 2+3=5 | Tier 3: weak reason; copy can't use the trigger |
| 19 | **CIPM ICE exhibitors and speakers** | Niche | Companies sponsoring an event | S5; HR lead | Sponsor, exhibitor and speaker pages on cipmnigeria.org [sm] N7 | Saw {{company}} at CIPM ICE; HR leaders there were asking about the new tax rules (INFERRED) | Once a year; next edition about Sep 2027 (INFERRED) | Med | 2+2=4 | Tier 3: annual, small, attendee list not public |
| 20 | **Champion migration** | Niche | Champion / user migration | All; past PaidHR admin users now at a new company | CRM export plus Clay job-change enrichment [sm] N9 | You ran payroll on PaidHR at {{old_company}}; set it up at {{new_company}} | Unknown | Blocked | n/a | Tier 3 until the CRM is available, then likely Tier 1 [sm] |
| 21 | **Closed-lost reactivation** | Focused | Closed lost reactivation | All; contact on the lost deal | HubSpot closed-lost deals, re-checked for a new signal (#1, #2, #6) | Something changed since we last spoke: the 2026 bands are live and the first annual return is due 31 January | Unknown | Blocked (needs CRM) | n/a | Tier 3 until the CRM is available |

**Not a campaign:** the PenCom defaulter list (signal-matrix N4) is used only as a priority flag inside #2 and #5. Copy never mentions it, because facts.md bans diagnosing the prospect.

---

## Campaign overviews (for the copywriter)

Claims, names and numbers come only from facts.md. Anything else renders as `{{placeholder}}`. All copy waits for `/build-workflow-spec` and `/campaign-copy`.

1. **January returns countdown.**
   - **Hook:** the 31 January deadline and the first full year on the new bands.
   - **How it runs:** a timing layer on the #2, #5 and #6 lists, sent 1 Dec to about 20 Jan. Email 1: the deadline, and that PaidHR is updated for the new law. Email 2: the 2025 remittance record ("₦934M in PAYE filed and ₦754M in pension processed in 2025, all on time"). Email 3: a soft CTA.
   - **Caution:** no penalty figures until checked against the statute [fa].
2. **HR and payroll hire.**
   - **Hook:** "Saw you're hiring a {{job_title}}."
   - **Variables:** job title, date posted, city.
   - **Message:** the new hire will own payroll on the 2026 bands; give them one platform from day one.
   - **Proof:** Nikky Taurus (faster request handling) or the 2025 remittance record.
   - **CTA:** offer a short look before the hire starts.
   - **Sends to:** the hiring manager, or the CEO if no HR lead exists.
3. **Remittance in the job description.**
   - **Hook:** quote one line the AI pulls from the job description ("prepare monthly PAYE and pension schedules").
   - **Message:** that task is what PaidHR automates.
   - **Proof:** "zero statutory defaults or delays".
   - **Difference from #2:** it only runs when the job description proves manual remittance work, so the hook is their own words.
4. **Fresh funding.**
   - **Hook:** the round, from the press item.
   - **Message:** the hiring plan that follows a raise.
   - **Proof:** Famasi (CEO-run payroll cut to under 5 minutes) and "backed by Accion Venture Lab" (shared investor-world trust).
   - **Who:** CEO only.
   - **Note:** low volume, so run it as a steady side workflow.
5. **First HR hire at an owner-run SME.**
   - **Hook:** "Looks like you're making your first HR hire."
   - **Message:** you've probably been running payroll yourself; Famasi's CEO did too.
   - **Variables:** job title, and confirmation that no HR title shows on LinkedIn.
   - **CTA:** have it set up before the hire's first payroll.
   - **The 10-minute rep test:** a rep would check LinkedIn for an HR person, see none, then see the job post. This automates exactly that.
6. **New HR or People leader.**
   - **Hook:** congratulations on the new role at {{company}}, plus their previous company.
   - **Message:** new leaders often pick the tools (Kredete's CEO introduced theirs and HR got more than payroll).
   - **CTA:** "what are you inheriting on payroll?"
   - **Who:** the leader only.
7. **New Finance lead or CFO.** Same structure as #6.
   - **Message:** 2026 bands applied correctly, remittances confirmed, journals pushed to the ERP.
   - **Proof:** ISO 27001 and NDPA, plus the 2025 remittance record.
   - **Gap:** there is no finance-buyer quote, so this is Tier 2.
8. **Frontline volume hiring, EWA.**
   - **Hook:** "{{open_role_count}} {{role_family}} roles open."
   - **Message:** frontline staff leave when pay runs out before month-end; EWA at no cost to your company, and you don't fund the advances. Add "over ₦400m disbursed through Earned Wage Access".
   - **Test:** send to a small batch first, since sector fit is INFERRED.
9. **Hiring velocity.**
   - **Hook:** the count of open roles.
   - **Message:** one record from offer to payslip.
   - **Difference from #2:** any roles count, not just HR, so the reason is broader and weaker.
10. **Multi-state hiring.**
    - **Hook:** the states named in their job posts.
    - **Message:** use the approved line "handles multi-state payroll and remits taxes and pensions in different states".
11. **Branch count.**
    - **Hook:** branch and state counts from Google Places.
    - **Message:** each state's PAYE goes to a different state tax office; one run covers all of them.
    - **QA:** check matches by hand on the first 50 rows before scaling.
12. **Payroll and accounting firms (non-ICP).**
    - **Hook:** the firm's own payroll services page.
    - **Message:** run client payroll and remittances on PaidHR under your own name.
    - **Partner-specific:** a different offer (Whitelabel), buyer and CTA, so its spec stays separate from the direct sequences.
    - **Before sending:** confirm with Product and Partnerships that Whitelabel is open beyond "Request Early Access".
13. **Creative ideas from their website.**
    - **Opener:** "I had a few ideas for {{company}}", then three bullets the AI writes from their site, each mapped to one module (Time & Attendance, multi-state remittance, EWA, PaidHiring).
    - **Guardrail:** the AI may only claim module features listed in [co] and facts.md.
    - **CTA:** "would any of these be useful?"
14. **NTA post engagers.**
    - **Hook:** name the topic, not the post ("the new PAYE rules").
    - **Message:** PaidHR is already updated for the new law.
    - **Before building:** check the Apify actor first.
15. **Cross-border hiring.**
    - **Hook:** the job posted in another country.
    - **Before copy:** cross-border claims need adding to facts.md first ("45+ currencies" conflicts across pages [fa]).
16. **Famasi lookalikes.**
    - **Hook:** "Companies like Famasi...", then the Famasi result.
    - **Seed:** Famasi, and Kredete once the CRM shows similar accounts.
    - **Re-score:** do it once the closed-won list exists; lookalikes of real best customers beat lookalikes of the three approved names.
17. **Headcount crossing 20.**
    - **Hook:** headcount growth.
    - **Message:** past 20 people, founder-run payroll starts costing hours; Famasi proof.
    - **Note:** keep at Tier 3 until LinkedIn headcount is checked against job posts.
18. **Rival tool in the job post.** Use only to route accounts to the S1 angle (remittances you can see confirmed). Never name the tool [fa].
19. **CIPM ICE exhibitors.** Build in Aug 2027 from the sponsor page; a one-off list.
20. **Champion migration.** Blocked. It goes to the top of the list once HubSpot can export past admin users [sm].
21. **Closed-lost reactivation.** Blocked. It needs HubSpot closed-lost deals with loss reasons.

---

## No-AI campaign

**January returns countdown, static version (idea 1 without the overlay data)**
- **Why it works without AI:** the deadline is the same for every Nigerian employer and public [mk]. The only variables are first name and company.
- **Core message:**
  - 3 short emails, from 1 Dec to mid Jan.
  - (1) "First annual return on the 2026 PAYE bands is due 31 January."
  - (2) "PaidHR is updated for the new law, and filed ₦934M in PAYE and ₦754M in pension in 2025, all on time."
  - (3) "Worth a 15-minute look before the deadline?"
- **List:** the S5 and S6 base list.

---

## Front-end offers

PaidHR's tiers start at 20 employees and prices aren't published [co]. A softer first step may convert cold leads better than "book a demo" (INFERRED).

1. **2026 PAYE band check.** Offer to run one sample payslip through the 2026 bands and show the deduction. It shows the product working on their own numbers.
   - **Needs:** Sales to confirm they can deliver it; it isn't a published offer.
2. **PaidRight 2026 salary report.** PaidHR's own pay benchmark (median ₦217,000 a month) [mk]. It's a low-ask CTA for #13, #14 and #17.
   - **Needs:** approval before quoting any figure from it; it isn't in facts.md yet.
3. **EWA pilot.** Switch on earned wage access for one team at no cost to the company [fa]. It lets employees feel the value fast, which suits #8.
   - **Needs:** Product to confirm whether EWA can run before a full payroll move.

---

## Recommendation: build #2 (HR and payroll hire), with #1 (January countdown) on top

**Why this one:**
- **Signal and data:** it has the strongest signal-and-data score among real lists: 17/20 in the signal matrix, R4 and D4 here.
- **Cost:** a Jobberman scrape at about $1 per 1,000 results [sm].
- **Reuse:** the same Clay build later feeds #3, #5, #8, #9, #10 and #18 with only filter changes. That's seven campaigns from one table.
- **Timing:** we have about three weeks before the 31 January window opens on 1 Dec. Adding #1 as the timing angle uses a deadline that won't come back until next year.
- **Proof fit:** it reaches S5 and S6, the two High-priority segments, where the approved proof (Famasi, Nikky Taurus, the remittance record) applies.

**Why not the others first:**
- #6 (new leader) is the best-supported story, but LinkedIn coverage of Nigerian SMEs is unproven. Build it second, reusing the people step from #2.
- #4 (funding) is clean but only about 9 accounts a month.

**Before launch:**
- Choose a sender and warm the sending inboxes (facts.md sender identity is open; gtm-system.md blockers).
- Run the scrape for a week and count the volume before committing.

**Next step:** `/build-workflow-spec` on idea 2, with the January overlay written into its routing and cadence.
