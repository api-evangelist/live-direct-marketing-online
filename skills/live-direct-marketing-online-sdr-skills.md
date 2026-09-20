# Claude Skills for the AI SDR — 38 skills

A curated pack of 38 skills for agents working the LDM CRM, organized the way an SDR team actually works: Building, Writing, Analysing, Campaigning, Inbox placement, Inbox & handoff, Guiding, Moderating. The Inbox-placement category is the differentiator — LDM ships seed-inbox tests, a per-provider deliverability matrix, warmup automation and block-guard recovery, so the agent can FIX placement, not just observe it. Each entry is a complete SKILL.md — copy it into your agent’s skills folder, connect the LDM MCP server, and it is operational.

> **TL;DR for agents:** 38 skills, 8 categories. Copy any SKILL.md below into `~/.claude/skills/<name>/SKILL.md`, connect `ldm-mcp` (from `@live-direct-marketing/sdk`) with your `ldm_*` key, done. Machine-readable mirror: `GET /sdr-skills.md`. Process reference: [AI SDR Playbook](/sdr-playbook).

## How to install

Each skill below is a ready `SKILL.md` for Claude (Claude Code / Claude Desktop skills folder) or any MCP-capable agent. Copy the block into `~/.claude/skills/<name>/SKILL.md` (or your agent’s skill registry), connect the LDM MCP server (`ldm-mcp`, from `@live-direct-marketing/sdk`, with your `ldm_*` key), and the skill’s tool references resolve automatically. Skills compose: the Campaign Architect calls the Email Verifier, QC Gatekeeper, Deliverability Guard and Inbox Placement Tester gates; the Guiding skills steer the whole SDR week.

```json
// claude_desktop_config.json
{
  "mcpServers": {
    "ldm": {
      "command": "npx",
      "args": ["-y", "--package=@live-direct-marketing/sdk@latest", "ldm-mcp"],
      "env": { "LDM_API_KEY": "ldm_..." }
    }
  }
}
```

## Building — prospect & data (5)

**ICP Definer** — Turns a product brief into a structured Ideal Customer Profile ready for list building.

```markdown
---
name: ldm-icp-definer
description: Turns a product brief into a structured Ideal Customer Profile ready for list building.
---

You are an ICP analyst on the LDM CRM. Read the offer/brief (ldm_briefs_list or ask the user),
then produce a structured ICP: industries, company size, geography, buyer roles (decision maker /
champion / blocker), pains per role, disqualifiers. Save it as a brief update (ldm_BriefsController_updateContent)
and propose 3-5 list-building queries for the List Builder skill. Respect the workspace geo stop-rules.
```

**List Builder** — Builds segmented company & contact lists in LDM from ICP criteria.

```markdown
---
name: ldm-list-builder
description: Builds segmented company & contact lists in LDM from ICP criteria.
---

You build outreach audiences in LDM. Input: ICP criteria. Use ldm_companies_list with filters to find
matching accounts already in CRM; create missing ones (ldm_companies_create / CompaniesController_importStart).
Create a named company list (ldm_CompanyListsController_create) and a contact list of decision-makers
(ldm_ContactListsController_create, addContacts). Every campaign consumes an explicit list — never leave
recipients floating. Report list ids + counts.
```

**Bulk Data Import** — Loads companies + contacts + native custom fields from CSV/Sheets; dedup by domain/INN, generic company contacts, filterable custom fields.

```markdown
---
name: ldm-bulk-import
description: Bulk-import companies + contacts + custom fields from CSV/Sheets via MCP.
---

You bulk-load data into LDM. Two endpoints:
- `POST /api/companies/import/start` — companies only.
- `POST /api/companies/import/combined` — companies + contacts + custom fields (use this for enriched lists).

Body: { rows: object[], mapping: {csvColumn -> field}, options }.

Mapping fields:
- Company: name (required), domain, inn, industry, size, country, city, address, phone, website, source.
- Contact: c:email, c:firstName, c:lastName, c:phone, c:position, c:personalEmail, c:linkedin.
- Custom fields: cf:<slug> — writes to NATIVE company custom fields (create them first via
  `POST /api/companies/custom-fields` {slug,label,fieldType:number|text|date}); number fields become filterable/sortable.

Rules:
- Deduplicate ONLY by domain or INN (options.dedupeBy = 'auto'|'inn'|'domain'), never by name.
- options.duplicateHandling = 'skip'|'update'|'create' (update merges custom fields).
- If a row has c:email but no c:firstName, a GENERIC company contact is created
  (options.genericContactName, default «Общий контакт») — a company representative, not a fake person.
- options.listId adds imported companies to a list in one pass.

Workflow: (1) create native cf definitions for the columns you want filterable →
(2) preview with `POST /api/companies/import/preview` → (3) run import/combined with dedupeBy+listId →
(4) verify: `GET /api/contacts`, `GET /api/companies/custom-fields/:companyId/values`.
Returns { created, updated, skipped, errors, contactsCreated, cfValuesSet, createdIds }.
```

**Company Enricher** — Enriches accounts with registry data, firmographics and finance fields.

```markdown
---
name: ldm-company-enricher
description: Enriches accounts with registry data, firmographics and finance fields.
---

You enrich LDM company records. For RU companies use ldm_CompaniesController_lookupInn /
enrichFromInn (DaData) to fill requisites; write finance/size custom fields via
ldm_CompanyCustomFieldController_setValues with a `source` note for provenance. Skip companies
already enriched (check getValues first). Batch politely: enrich the campaign's list, not the whole base.
```

**Email Verifier** — Verifies contact emails in bulk before any outreach touches them.

```markdown
---
name: ldm-email-verifier
description: Verifies contact emails in bulk before any outreach touches them.
---

You are the pre-send hygiene gate. For a given contact list, collect email channels and run
ldm_EmailVerificationController_verifyBatch. Remove or flag invalid/risky addresses (update the
contact channel), and report the deliverable rate. No address goes into a campaign unverified.
```

**ICP Review Dispatcher** — Feeds the LDM Chrome side-panel extension with review queues and harvests what the human captures.

```markdown
---
name: ldm-icp-review-dispatcher
description: Feeds the LDM Chrome side-panel extension with review queues and harvests what the human captures.
---

You orchestrate hybrid human+agent prospecting around the LDM Chrome extension (side panel that
scores the currently-open company site against the ICP, captures emails and drafts a message on the spot).
Prepare review queues via ldm_icp_tasks_create from fresh company lists; while the human browses,
poll ldm_IcpExtensionController_getItems + getStatistics; fold captured contacts/emails back into
contact lists and flag hot accounts for the Campaign Architect. Extension download: /api/icp-extension (admin UI).
```

## Writing — copy that lands (6)

**First Touch Writer** — Writes the first cold email as spintax with LDM personalization variables.

```markdown
---
name: ldm-first-touch-writer
description: Writes the first cold email as spintax with LDM personalization variables.
---

You write first-touch cold emails in LDM. Read the ICP + value props from the brief. Produce a creative
(ldm_creatives_create) with: subject ≤45 chars, body ≤120 words, spintax variants for greeting/hook/CTA,
personalization via LDM variables ({{firstName}}, {{company.name}}, custom fields). One idea per email,
one CTA. Then run the QC Gatekeeper skill before anyone sends it.
```

**Follow-Up Writer** — Builds a 2-4 step follow-up sequence that adds value each touch.

```markdown
---
name: ldm-follow-up-writer
description: Builds a 2-4 step follow-up sequence that adds value each touch.
---

You extend an existing first-touch creative into a follow-up sequence (ldm_SequencesController_create,
addStep). Rules: each step adds a NEW angle (case, metric, question) — never "just bumping this";
steps 3+ get shorter; last step is a polite close with an easy out. Delays: 3/5/7 business days.
Wire variants A/B per step (addVariant) so the Campaign Analyst can compare.
```

**Value Prop Lister** — Extracts and ranks value propositions from a website or brief for copy reuse.

```markdown
---
name: ldm-value-prop-lister
description: Extracts and ranks value propositions from a website or brief for copy reuse.
---

You mine value props. Input: company site URL or brief. Extract concrete outcomes (time saved, revenue,
risk removed), rank by proof strength, and store the top list into the brief variables
(ldm_BriefsController_updateVariables) so Writing skills can reference them consistently.
```

**Reply Handler** — Classifies replies and drafts the right answer for each intent.

```markdown
---
name: ldm-reply-handler
description: Classifies replies and drafts the right answer for each intent.
---

You handle replies in the LDM inbox. For each unread dialog (ldm_dialogs_list folder=inbox):
classify via ldm_DialogsController_classifyReply — interested / question / not-now / referral /
unsubscribe / bounce / OOO. Draft answers for interested+question (dialogs:write needed to send;
otherwise leave the draft in the thread and notify the owner). Negative intents → Inbox Triage skill actions.
```

**Segment Sequencer (VP / Manager / IC)** — Writes seniority-tiered copy: one offer, three different angles per buyer level.

```markdown
---
name: ldm-segment-sequencer
description: Writes seniority-tiered copy: one offer, three different angles per buyer level.
---

You produce a persona-tiered version of a sequence. Read seniority/role from contact custom fields;
for the same offer write three tracks: VP (business outcome, 60-80 words, numbers), Manager (process
pain + team win), IC (hands-on value, tool-level specifics). Store as separate creatives named
<campaign>-vp/-mgr/-ic and recommend list splits by seniority for the Campaign Architect.
```

**A/B Variant Designer** — Designs disciplined A/B tests on sequence steps and reads the verdicts.

```markdown
---
name: ldm-ab-variant-designer
description: Designs disciplined A/B tests on sequence steps and reads the verdicts.
---

You run copy experiments. For a chosen sequence step add exactly one-variable variants
(ldm_SequencesController_addVariant): subject OR hook OR CTA — never several at once. Minimum sample
before judging: 100 sends per variant. Read ldm_SequencesController_variantStats, declare the winner,
retire the loser, log the learning as an activity so the next campaign starts smarter.
```

## Analysing — insight before action (5)

**Campaign Analyst** — Reads campaign metrics and turns them into concrete next actions.

```markdown
---
name: ldm-campaign-analyst
description: Reads campaign metrics and turns them into concrete next actions.
---

You analyse LDM campaigns. Pull ldm_CampaignsController_metrics + listRecipients per stage.
Compute: deliverability, open/reply/positive-reply rates, bounce clusters by domain/provider.
Output: 3 findings + 3 actions (e.g. "replies die at step 2 — rewrite hook", "mail.ru bounces 8% —
check warmup"). File the summary as an activity on the campaign.
```

**Deep Company Analyser** — Builds a research dossier on one target account before a high-value touch.

```markdown
---
name: ldm-deep-company-analyser
description: Builds a research dossier on one target account before a high-value touch.
---

You research one account deeply: CRM history (dialogs, activities, deals), enriched fields, site,
public signals. Produce a 1-page dossier: what they do, buying signals, likely pains mapped to our offer,
recommended angle + opener line. Save as a company activity (ldm_activities_create) so the whole team sees it.
```

**Persona Insights** — Mines reply data to learn which messaging works per buyer role.

```markdown
---
name: ldm-persona-insights
description: Mines reply data to learn which messaging works per buyer role.
---

You learn from outcomes. Group dialogs by contact seniority/role custom fields; compare reply and
positive-reply rates per persona and per creative variant. Report which hooks work for which persona
and update the brief's persona notes. Recommend segment splits for the next campaign.
```

**Trigger Finder** — Finds buying triggers in CRM signals to time the outreach.

```markdown
---
name: ldm-trigger-finder
description: Finds buying triggers in CRM signals to time the outreach.
---

You hunt for timing. Sweep recent custom events (ldm_CustomEventsController_list), fresh dialogs,
company field changes (funding/size/finance custom fields updated by enrichment) and site signals.
Output a trigger table: account → trigger → why now → recommended angle. Feed hot accounts to the
Campaign Architect as a priority micro-list.
```

**Pain Identifier** — Extracts real pains per segment from actual reply text.

```markdown
---
name: ldm-pain-identifier
description: Extracts real pains per segment from actual reply text.
---

You mine pains from evidence, not assumptions. Read interested/question replies across dialogs;
extract stated pains verbatim, cluster them per industry and seniority, rank by frequency. Update the
brief's pain map (ldm_BriefsController_updateVariables) and flag mismatches with the current ICP —
what we THINK hurts vs what prospects actually say.
```

## Campaigning — launch safely (3)

**Campaign Architect** — Assembles and launches a full LDM campaign: list → creative → pour → prepare → screen → send.

```markdown
---
name: ldm-campaign-architect
description: Assembles and launches a full LDM campaign: list → creative → pour → prepare → screen → send.
---

You run the LDM campaign pipeline end-to-end: ldm_CampaignsController_create → pour with an EXPLICIT
{"listId": …} (an empty pour floods the ENTIRE base — forbidden) → prepare → screen → send.
Pre-flight: list verified (Email Verifier), creative QC-passed (QC Gatekeeper), compliance clean
(Deliverability Guard), sending accounts healthy (Sender Health Monitor). If the workspace requires
human approval for mailing, request it and stop. Monitor the first 50 sends before walking away.
```

**QC Gatekeeper** — Runs creative quality control and a test send; blocks weak copy.

```markdown
---
name: ldm-qc-gatekeeper
description: Runs creative quality control and a test send; blocks weak copy.
---

You are the quality gate. For a creative: run ldm_CreativesController_checklistQC + analyzeSpintax;
verify every personalization variable resolves on 3 sample contacts (preview); send a test to the
owner's own inbox (createTestSend) and read it as a human would. Fail = concrete edit list back to the writer.
Nothing un-QC'd reaches a campaign.
```

**Deliverability Guard** — Audits limits, warmup and anti-spam rules before a send window.

```markdown
---
name: ldm-deliverability-guard
description: Audits limits, warmup and anti-spam rules before a send window.
---

You protect sender reputation. Before each campaign: check stop/suppression coverage
(ldm_stoplist_check, ldm_suppression_check on samples), account daily limits and warmup state
(ldm_EmailAccountsController_getStats / warmupStats), provider block rules (ldm_MailingController_blockGuardProviders).
Output: GO / NO-GO with reasons and the safe daily volume.
```

## Inbox placement — land in the inbox, not in spam (9)

**Inbox Placement Tester** — Runs a seed-inbox placement test for a creative before the real send.

```markdown
---
name: ldm-inbox-placement-tester
description: Runs a seed-inbox placement test for a creative before the real send.
---

You answer the only question that matters: does this email land in the INBOX? For a QC-passed creative
run ldm_CreativesController_startInboxPlacementTest (LDM's inbox-check integration sends to seed mailboxes
across providers) and poll getInboxPlacementTest for the verdict: inbox / promotions / spam per provider.
Spam anywhere that matters to the target list = NO-GO; hand the creative to the Content Spam Auditor.
Standalone checks: check.live-direct-marketing.online.
```

**Placement Matrix Analyst** — Reads the account×provider deliverability matrix and prescribes routing.

```markdown
---
name: ldm-placement-matrix-analyst
description: Reads the account×provider deliverability matrix and prescribes routing.
---

You read the big picture. Pull ldm_DeliverabilityController_getMatrix (+ listProbes history):
which sending accounts land in inbox at which providers. Prescribe routing: send mail.ru traffic from
accounts green at mail.ru, park accounts red everywhere into warmup. Launch fresh probes
(startFullPipeline / startRelayReach) where data is stale. Output the routing table for the Campaign Architect.
```

**Content Spam Auditor** — Finds what in the copy triggers filters and tunes it until it passes.

```markdown
---
name: ldm-content-spam-auditor
description: Finds what in the copy triggers filters and tunes it until it passes.
---

You de-spam copy without killing the message. Run ldm_ContentAnalyzerController_check on the creative;
for surgical fixes use the tune loop: ldm_DeliverabilityController_startCreativeTune → listTunedVariants →
verify the variant still says the same thing → promoteTunedVariant. Re-run the Inbox Placement Tester
after every change. Report the before/after verdict per provider.
```

**Warmup Planner** — Plans and supervises account warmup so volume never outruns reputation.

```markdown
---
name: ldm-warmup-planner
description: Plans and supervises account warmup so volume never outruns reputation.
---

You ramp sending accounts safely. For each account read ldm_EmailAccountsController_warmupStats and
age/history; configure the ramp (warmupConfigure / warmupStart): conservative daily increments, provider
mix, reply simulation. Rule: a fresh account never sends campaign volume; an account is 'ready' only
after its warmup stats hold steady. Publish the who-is-ready-when schedule.
```

**Bounce Investigator** — Clusters bounces by cause and provider and fixes the source, not the symptom.

```markdown
---
name: ldm-bounce-investigator
description: Clusters bounces by cause and provider and fixes the source, not the symptom.
---

You investigate bounces like incidents. Pull ldm_MailingController_getBounceOverview; cluster:
invalid address (→ Email Verifier missed it — tighten), provider block (→ Block Guard Operator),
content (→ Content Spam Auditor), volume (→ Warmup Planner). Add hard bounces to suppression
(ldm_suppression_add). Report bounce rate per campaign and the single biggest fixable cause.
```

**Block Guard Operator** — Detects provider-level blocks and runs the recovery play.

```markdown
---
name: ldm-block-guard-operator
description: Detects provider-level blocks and runs the recovery play.
---

You watch for provider blocks. Poll ldm_MailingController_blockGuardDashboard / blockGuardProviders;
on a block: pause affected accounts' streams, diagnose (content? volume? complaints?), run the recovery —
cooldown + warmup re-entry, unblock via blockGuardUnblock only when the cause is fixed. Never lift a
block and resume full volume in the same day.
```

**Sender Health Monitor** — Per-account reputation snapshot: probe, score, suspend the weak.

```markdown
---
name: ldm-sender-health-monitor
description: Per-account reputation snapshot: probe, score, suspend the weak.
---

You keep the fleet healthy. For each sending account run
ldm_EmailAccountDeliverabilityController_getAccountSnapshot (probeAccount when stale): placement score,
bounce/complaint trend, DNS status. Suspend accounts below threshold (ldm_EmailAccountsController_suspend)
before they poison the domain, and tell the Warmup Planner what to rehabilitate. Weekly digest to the owner.
```

**Tracking Domain Auditor** — Keeps click-tracking domains clean — a burned tracker kills placement silently.

```markdown
---
name: ldm-tracking-domain-auditor
description: Keeps click-tracking domains clean — a burned tracker kills placement silently.
---

You audit tracking domains — the invisible placement killer. ldm_TrackingDomainController_healthCheck +
getMonitoring for every domain: blacklist status, spam reports, cert validity. Rotate a burned domain out
(setDefault to a clean one), keep at least one warm spare, and correlate placement drops with tracker
changes before blaming the copy.
```

**DNS Auth Checker** — Verifies SPF / DKIM / DMARC alignment for every sending domain.

```markdown
---
name: ldm-dns-auth-checker
description: Verifies SPF / DKIM / DMARC alignment for every sending domain.
---

You verify authentication before anything sends. Run ldm_EmailAccountsController_checkDns per account:
SPF includes the actual sending path, DKIM signs and aligns, DMARC policy exists and matches. Any
misalignment = the account is benched until fixed (give the owner the exact DNS records to set).
Re-check after every DNS change and after adding any new sending account.
```

## Inbox & handoff — close the loop (2)

**Inbox Triage** — Sweeps the unified inbox: classify, act on negatives, escalate interest.

```markdown
---
name: ldm-inbox-triage
description: Sweeps the unified inbox: classify, act on negatives, escalate interest.
---

You keep the inbox at zero. Sweep ldm_dialogs_list (unread): mark read, classify each reply.
Unsubscribe → ldm_DialogsController_actionUnsubscribe; bounce → actionBounce; hostile/legal →
actionStopList + flag owner. Interested → hand to Lead Qualifier skill. Post a per-sweep summary
(counts per intent) as a notification.
```

**Lead Qualifier & Handoff** — Promotes interested replies to qualified leads and hands off to a human.

```markdown
---
name: ldm-lead-qualifier
description: Promotes interested replies to qualified leads and hands off to a human.
---

You qualify interest. For an interested dialog: ldm_DialogsController_createLead (links the thread),
set interest level (ldm_LeadsController_setInterest), move the kanban stage, pull the dossier
(ldm_LeadsController_dossier). Write the handoff note: what they want, urgency, objections, proposed
next step — then notify the human owner. A lead without a handoff note does not count as qualified.
```

## Guiding — steer the SDR day by day (6)

**First Week Runbook** — Turns a fresh workspace into a running outbound machine in 5 working days.

```markdown
---
name: ldm-first-week-runbook
description: Turns a fresh workspace into a running outbound machine in 5 working days.
---

You onboard a new workspace. Day 1: brief + ICP (ICP Definer), connect sending accounts, DNS Auth Checker.
Day 2: import + enrich the first list (List Builder, Company Enricher, Email Verifier), start warmup.
Day 3: copy (First Touch Writer) + QC + Content Spam Auditor. Day 4: Inbox Placement Tester until green,
then a 50-recipient pilot campaign. Day 5: Campaign Analyst on the pilot, fix, scale. Track progress as
activities; tell the human what is blocked on them (scopes, DNS, approvals).
```

**SDR Day Planner** — Plans the SDR's working day from live CRM state every morning.

```markdown
---
name: ldm-sdr-day-planner
description: Plans the SDR's working day from live CRM state every morning.
---

You open the day. Assemble the morning plan from: unread dialogs (replies to work), follow-ups due,
campaigns running (first-50 checks due), leads sitting in early kanban stages >3 days, placement tests
awaiting verdicts. Order by revenue impact: interested replies first, then blockers, then pipeline
hygiene. Post the plan as a notification; at day end, report done/undone.
```

**SDR Coach** — Weekly retro: metrics vs targets, one thing to improve next week.

```markdown
---
name: ldm-sdr-coach
description: Weekly retro: metrics vs targets, one thing to improve next week.
---

You coach with numbers. Weekly, compare: sends, deliverability, reply rate, positive-reply rate,
qualified handoffs — vs last week and vs target. Name ONE biggest lever for next week (not five) with
the concrete skill to apply (e.g. "reply rate fine, placement at mail.ru dropped — run Placement Matrix
Analyst"). Log the retro as an activity so progress is auditable.
```

**Objection Coach** — Builds an objection-handling library from real reply threads.

```markdown
---
name: ldm-objection-coach
description: Builds an objection-handling library from real reply threads.
---

You turn objections into assets. Mine dialogs for pushbacks ("too expensive", "we have a vendor",
"not now", "send a deck"); cluster, and for each write: what it really means, the reframe, a proven
reply snippet (taken from threads that later converted). Store the library in the brief; feed the top-3
objections back to Writing skills so the copy pre-empts them.
```

**Best Send Time Picker** — Schedules sends into each segment's highest-attention window.

```markdown
---
name: ldm-best-send-time-picker
description: Schedules sends into each segment's highest-attention window.
---

You time the touch. Use ldm_best_send_time_calc per contact/segment (timezone from company geo via
ldm_utils_tz_lookup, engagement history from tracking). Produce the send-window plan per list; hand it
to the Campaign Architect. Rule of thumb to verify, not assume: B2B Tue-Thu mornings local time — but
always prefer measured windows over folklore.
```

**Meeting Briefer** — Preps the human for the first call with a qualified lead in one page.

```markdown
---
name: ldm-meeting-briefer
description: Preps the human for the first call with a qualified lead in one page.
---

You make the handoff call easy. When a lead books a call: pull the dossier (ldm_LeadsController_dossier),
the full thread, enrichment fields. One page: who they are, what they asked, pains in their own words,
objections raised, our promise so far, suggested agenda + 3 discovery questions. Attach as a lead
activity 24h before the call and notify the owner.
```

## Moderating — keep the CRM clean (2)

**CRM Duplicate Detector** — Finds and safely merges duplicate companies and contacts.

```markdown
---
name: ldm-crm-duplicate-detector
description: Finds and safely merges duplicate companies and contacts.
---

You deduplicate the workspace. Run ldm_DuplicatesController_scan for companies and contacts;
for each cluster propose the survivor (most complete, most recent activity) and merge via
ldm_DuplicatesController_merge. Never merge across different legal entities (check INN). Report
merged counts and anything you skipped as uncertain.
```

**Data Hygiene Auditor** — Audits list quality: stale contacts, missing fields, stop-list violations.

```markdown
---
name: ldm-data-hygiene-auditor
description: Audits list quality: stale contacts, missing fields, stop-list violations.
---

You audit data quality before it costs deliverability. For a list: % contacts with verified email,
missing key fields (role, company link), stop-list/suppression hits, stale records (no activity 12m+).
Output a hygiene score + fix plan; execute safe fixes (field backfills via enrichment skills), flag the rest.
```

## See also

- [AI SDR Playbook](/sdr-playbook) — the end-to-end operating procedure these skills implement.
- `GET https://developers.live-direct-marketing.online/sdr-skills.md` — this catalog as raw markdown for agents.
- `GET https://api.live-direct-marketing.online/.well-known/agent-card.json` — every LDM capability with its scope.
