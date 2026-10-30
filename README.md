# Live Direct Marketing

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Live Direct Marketing (LDM) is a B2B outreach and CRM platform built to be operated by AI agents: the same Bearer-authenticated HTTPS surface serves the web UI, MCP clients and A2A peers. The LDM v3 API publishes an OpenAPI 3.0 contract with 1,304 operations across 119 tags (companies, contacts, leads, pipelines, campaigns, creatives, mailboxes, deliverability probes, suppression and stop-lists, webhooks, billing, DSAR) and a remote Streamable-HTTP MCP server with an anonymous bootstrap (ldm_terms / ldm_register) that mints a scoped ldm_* key without a human. A second product, Inbox Check, is a free inbox-placement test with its own 196-operation OpenAPI, a remote MCP server and an A2A agent card at check.live-direct-marketing.online. Billing is per confirmed inbox delivery ($0.015 managed / $0.005 BYOC), read from a public pricing endpoint. The operator is a Russian entity (OOO LDM, Yaroslavl); legal documents are drafts pending lawyer review.

**Areas:** Company · Email · Email Deliverability · Sales & marketing automation · CRM · Lead Management · Cold Outreach · Agent-Native · MCP · A2A · Webhook · B2B

## Live Direct Marketing on APIs.io

Everything profiled for Live Direct Marketing is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/live-direct-marketing-online/](https://apis.io/providers/live-direct-marketing-online/)** — or go straight to one of the APIs or properties below.

### APIs (150)

- [LDM MCP Server](https://apis.io/apis/live-direct-marketing-online/ldm-mcp-server/) — Remote Streamable-HTTP MCP server at https://api.live-direct-marketing.online/mcp (protocol 2025-06-18, server ldm-delivery 0.6.1). An anonymous session…
- [LDM.delivery A2A Agent](https://apis.io/apis/live-direct-marketing-online/ldm-a2a-agent/) — A2A 0.3.0-shaped agent card served at https://api.live-direct-marketing.online/.well-known/agent.json (237 curated skills of 1,270, ?full=1 for all;…
- [LDM Webhook Events](https://apis.io/apis/live-direct-marketing-online/ldm-webhook-events/) — Outbound HTTPS webhook subscriptions for lead, dialog and task events (lead.created, lead.moved, lead.won, lead.lost, dialog.received, dialog.replied,…
- [Inbox Check MCP Server](https://apis.io/apis/live-direct-marketing-online/inbox-check-mcp-server/) — Remote Streamable-HTTP MCP server at https://check.live-direct-marketing.online/mcp requiring Authorization: Bearer icp_live_* (anonymous tools/list answers…
- [Inbox Check A2A Agent Card](https://apis.io/apis/live-direct-marketing-online/inbox-check-a2a-agent/) — Provider-shaped agent card at https://check.live-direct-marketing.online/.well-known/agent.json listing 21 REST-bound skills with HTTP method, URL and…
- [Live Direct Marketing A2A API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-a2a-api/) — The A2A API from Live Direct Marketing — 1 operation(s) for a2a.
- [Live Direct Marketing Account API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-account-api/) — The account API from Live Direct Marketing — 4 operation(s) for account.
- [Live Direct Marketing Activities API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-activities-api/) — The Activities API from Live Direct Marketing — 3 operation(s) for activities.
- [Live Direct Marketing Admin API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-admin-api/) — The admin API from Live Direct Marketing — 123 operation(s) for admin.
- [Live Direct Marketing Admin / Honeypot API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-admin-honeypot-api/) — The Admin / Honeypot API from Live Direct Marketing — 5 operation(s) for admin / honeypot.
- [Live Direct Marketing Admin RPA API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-admin-rpa-api/) — The Admin RPA API from Live Direct Marketing — 11 operation(s) for admin rpa.
- [Live Direct Marketing Agency API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-agency-api/) — The Agency API from Live Direct Marketing — 3 operation(s) for agency.
- [Live Direct Marketing Agent Card API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-agent-card-api/) — The Agent Card API from Live Direct Marketing — 8 operation(s) for agent card.
- [Live Direct Marketing AI API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-ai-api/) — The AI API from Live Direct Marketing — 8 operation(s) for ai.
- [Live Direct Marketing Allowlist API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-allowlist-api/) — The Allowlist API from Live Direct Marketing — 4 operation(s) for allowlist.
- [Live Direct Marketing Amo Widget API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-amo-widget-api/) — The amo-widget API from Live Direct Marketing — 7 operation(s) for amo-widget.
- [Live Direct Marketing API Keys (tenant-scoped) API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-api-keys-tenant-scoped-api/) — The API Keys (tenant-scoped) API from Live Direct Marketing — 6 operation(s) for api keys (tenant-scoped).
- [Live Direct Marketing Audit API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-audit-api/) — The Audit API from Live Direct Marketing — 2 operation(s) for audit.
- [Live Direct Marketing Auth API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-auth-api/) — The auth API from Live Direct Marketing — 8 operation(s) for auth.
- [Live Direct Marketing Authentication API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-authentication-api/) — The Authentication API from Live Direct Marketing — 13 operation(s) for authentication.
- [Live Direct Marketing Best Send Time API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-best-send-time-api/) — The Best Send Time API from Live Direct Marketing — 1 operation(s) for best send time.
- [Live Direct Marketing Beta Signups API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-beta-signups-api/) — The beta-signups API from Live Direct Marketing — 1 operation(s) for beta-signups.
- [Live Direct Marketing Billing API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-billing-api/) — The Billing API from Live Direct Marketing — 2 operation(s) for billing.
- [Live Direct Marketing Branding API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-branding-api/) — The Branding API from Live Direct Marketing — 1 operation(s) for branding.
- [Live Direct Marketing Briefs API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-briefs-api/) — The Briefs API from Live Direct Marketing — 23 operation(s) for briefs.
- [Live Direct Marketing Browser Queue API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-browser-queue-api/) — The Browser Queue API from Live Direct Marketing — 6 operation(s) for browser queue.
- [Live Direct Marketing Campaign Groups API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-campaign-groups-api/) — The Campaign Groups API from Live Direct Marketing — 3 operation(s) for campaign groups.
- [Live Direct Marketing Campaigns API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-campaigns-api/) — The Campaigns API from Live Direct Marketing — 38 operation(s) for campaigns.
- [Live Direct Marketing Canvas API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-canvas-api/) — The Canvas API from Live Direct Marketing — 4 operation(s) for canvas.
- [Live Direct Marketing Cohort Metrics API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-cohort-metrics-api/) — The Cohort Metrics API from Live Direct Marketing — 3 operation(s) for cohort metrics.
- [Live Direct Marketing Companies API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-companies-api/) — The Companies API from Live Direct Marketing — 19 operation(s) for companies.
- [Live Direct Marketing Companies / Custom Fields API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-companies-custom-fields-api/) — The Companies / Custom Fields API from Live Direct Marketing — 4 operation(s) for companies / custom fields.
- [Live Direct Marketing Companies / Duplicates API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-companies-duplicates-api/) — The Companies / Duplicates API from Live Direct Marketing — 5 operation(s) for companies / duplicates.
- [Live Direct Marketing Company List Groups API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-company-list-groups-api/) — The Company List Groups API from Live Direct Marketing — 3 operation(s) for company list groups.
- [Live Direct Marketing Company Lists API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-company-lists-api/) — The Company Lists API from Live Direct Marketing — 7 operation(s) for company lists.
- [Live Direct Marketing Connectors API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-connectors-api/) — The Connectors API from Live Direct Marketing — 2 operation(s) for connectors.
- [Live Direct Marketing Contact List Groups API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-contact-list-groups-api/) — The Contact List Groups API from Live Direct Marketing — 3 operation(s) for contact list groups.
- [Live Direct Marketing Contact Lists API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-contact-lists-api/) — The Contact Lists API from Live Direct Marketing — 8 operation(s) for contact lists.
- [Live Direct Marketing Contacts API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-contacts-api/) — The Contacts API from Live Direct Marketing — 19 operation(s) for contacts.
- [Live Direct Marketing Content Analyzer API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-content-analyzer-api/) — The Content Analyzer API from Live Direct Marketing — 1 operation(s) for content analyzer.
- [Live Direct Marketing Creatives API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-creatives-api/) — The Creatives API from Live Direct Marketing — 90 operation(s) for creatives.
- [Live Direct Marketing Creatives / On-Demand API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-creatives-on-demand-api/) — The Creatives / On-Demand API from Live Direct Marketing — 6 operation(s) for creatives / on-demand.
- [Live Direct Marketing Custom Events API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-custom-events-api/) — The Custom Events API from Live Direct Marketing — 3 operation(s) for custom events.
- [Live Direct Marketing Custom Extract API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-custom-extract-api/) — The Custom Extract API from Live Direct Marketing — 2 operation(s) for custom extract.
- [Live Direct Marketing Custom Fields API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-custom-fields-api/) — The Custom Fields API from Live Direct Marketing — 6 operation(s) for custom fields.
- [Live Direct Marketing Custom Objects API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-custom-objects-api/) — The Custom Objects API from Live Direct Marketing — 4 operation(s) for custom objects.
- [Live Direct Marketing Deliverability API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-deliverability-api/) — The Deliverability API from Live Direct Marketing — 11 operation(s) for deliverability.
- [Live Direct Marketing Deploy API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-deploy-api/) — The deploy API from Live Direct Marketing — 2 operation(s) for deploy.
- [Live Direct Marketing Development Pipeline API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-development-pipeline-api/) — The Development Pipeline API from Live Direct Marketing — 13 operation(s) for development pipeline.
- [Live Direct Marketing Development Pipeline — Conveyor Bridge API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-development-pipeline-conveyor-bridge-api/) — The Development Pipeline — Conveyor Bridge API from Live Direct Marketing — 5 operation(s) for development pipeline — conveyor bridge.
- [Live Direct Marketing Dialog Linker API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-dialog-linker-api/) — The Dialog Linker API from Live Direct Marketing — 6 operation(s) for dialog linker.
- [Live Direct Marketing Dialogs API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-dialogs-api/) — The Dialogs API from Live Direct Marketing — 44 operation(s) for dialogs.
- [Live Direct Marketing Domain Watch API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-domain-watch-api/) — The domain-watch API from Live Direct Marketing — 7 operation(s) for domain-watch.
- [Live Direct Marketing Domain Observations API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-domainobservations-api/) — The DomainObservations API from Live Direct Marketing — 6 operation(s) for domainobservations.
- [Live Direct Marketing Domains API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-domains-api/) — The Domains API from Live Direct Marketing — 2 operation(s) for domains.
- [Live Direct Marketing Domain Watch Placement API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-domainwatchplacement-api/) — The DomainWatchPlacement API from Live Direct Marketing — 1 operation(s) for domainwatchplacement.
- [Live Direct Marketing DSAR API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-dsar-api/) — The DSAR API from Live Direct Marketing — 3 operation(s) for dsar.
- [Live Direct Marketing Email Accounts API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-email-accounts-api/) — The Email Accounts API from Live Direct Marketing — 34 operation(s) for email accounts.
- [Live Direct Marketing Email Accounts — Deliverability API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-email-accounts-deliverability-api/) — The Email Accounts — Deliverability API from Live Direct Marketing — 3 operation(s) for email accounts — deliverability.
- [Live Direct Marketing Email Accounts / GAS Webhook API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-email-accounts-gas-webhook-api/) — The Email Accounts / GAS Webhook API from Live Direct Marketing — 1 operation(s) for email accounts / gas webhook.
- [Live Direct Marketing Email Accounts / Inbox Ingest API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-email-accounts-inbox-ingest-api/) — The Email Accounts / Inbox Ingest API from Live Direct Marketing — 1 operation(s) for email accounts / inbox ingest.
- [Live Direct Marketing Email Verification API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-email-verification-api/) — The Email Verification API from Live Direct Marketing — 2 operation(s) for email verification.
- [Live Direct Marketing Enrichment API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-enrichment-api/) — The Enrichment API from Live Direct Marketing — 2 operation(s) for enrichment.
- [Live Direct Marketing Exports API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-exports-api/) — The Exports API from Live Direct Marketing — 4 operation(s) for exports.
- [Live Direct Marketing Feedback API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-feedback-api/) — The feedback API from Live Direct Marketing — 1 operation(s) for feedback.
- [Live Direct Marketing Files API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-files-api/) — The Files API from Live Direct Marketing — 15 operation(s) for files.
- [Live Direct Marketing Files / Serve API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-files-serve-api/) — The Files / Serve API from Live Direct Marketing — 4 operation(s) for files / serve.
- [Live Direct Marketing Health API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-health-api/) — The health API from Live Direct Marketing — 2 operation(s) for health.
- [Live Direct Marketing ICP Extension / API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-icp-extension-api-api/) — The ICP Extension / API API from Live Direct Marketing — 17 operation(s) for icp extension / api.
- [Live Direct Marketing ICP Extension API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-icp-extension-api/) — The ICP Extension API from Live Direct Marketing — 14 operation(s) for icp extension.
- [Live Direct Marketing IMAP Orchestrator API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-imap-orchestrator-api/) — The IMAP Orchestrator API from Live Direct Marketing — 24 operation(s) for imap orchestrator.
- [Live Direct Marketing Import API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-import-api/) — The Import API from Live Direct Marketing — 10 operation(s) for import.
- [Live Direct Marketing Inbound Rules API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-inbound-rules-api/) — The Inbound Rules API from Live Direct Marketing — 7 operation(s) for inbound rules.
- [Live Direct Marketing Jobs API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-jobs-api/) — The Jobs API from Live Direct Marketing — 1 operation(s) for jobs.
- [Live Direct Marketing Landing API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-landing-api/) — The Landing API from Live Direct Marketing — 1 operation(s) for landing.
- [Live Direct Marketing Leads API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-leads-api/) — The Leads API from Live Direct Marketing — 21 operation(s) for leads.
- [Live Direct Marketing Legal API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-legal-api/) — The Legal API from Live Direct Marketing — 8 operation(s) for legal.
- [Live Direct Marketing LinkedIn / Extension API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-linkedin-extension-api-api/) — The LinkedIn / Extension API API from Live Direct Marketing — 6 operation(s) for linkedin / extension api.
- [Live Direct Marketing Mail Agent API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-mail-agent-api/) — The Mail Agent API from Live Direct Marketing — 7 operation(s) for mail agent.
- [Live Direct Marketing Mail Agent / Update API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-mail-agent-update-api/) — The Mail Agent / Update API from Live Direct Marketing — 1 operation(s) for mail agent / update.
- [Live Direct Marketing Mail Routing Rules API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-mail-routing-rules-api/) — The Mail Routing Rules API from Live Direct Marketing — 4 operation(s) for mail routing rules.
- [Live Direct Marketing Mail Transport API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-mail-transport-api/) — The Mail Transport API from Live Direct Marketing — 1 operation(s) for mail transport.
- [Live Direct Marketing Mailing API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-mailing-api/) — The Mailing API from Live Direct Marketing — 39 operation(s) for mailing.
- [Live Direct Marketing Marking API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-marking-api/) — The Marking API from Live Direct Marketing — 5 operation(s) for marking.
- [Live Direct Marketing MCP Transport API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-mcp-transport-api/) — The mcp-transport API from Live Direct Marketing — 2 operation(s) for mcp-transport.
- [Live Direct Marketing Monitoring API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-monitoring-api/) — The monitoring API from Live Direct Marketing — 16 operation(s) for monitoring.
- [Live Direct Marketing Monitoring Enrollment API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-monitoring-enrollment-api/) — The monitoring-enrollment API from Live Direct Marketing — 1 operation(s) for monitoring-enrollment.
- [Live Direct Marketing Nalog ID API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-nalog-id-api/) — The Nalog ID API from Live Direct Marketing — 2 operation(s) for nalog id.
- [Live Direct Marketing Names API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-names-api/) — The Names API from Live Direct Marketing — 2 operation(s) for names.
- [Live Direct Marketing Notifications API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-notifications-api/) — The Notifications API from Live Direct Marketing — 10 operation(s) for notifications.
- [Live Direct Marketing OAuth API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-oauth-api/) — The oauth API from Live Direct Marketing — 10 operation(s) for oauth.
- [Live Direct Marketing OAUTH Tests API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-oauth-tests-api/) — The oauth-tests API from Live Direct Marketing — 2 operation(s) for oauth-tests.
- [Live Direct Marketing Observability / API Monitor API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-observability-api-monitor-api/) — The Observability / API Monitor API from Live Direct Marketing — 6 operation(s) for observability / api monitor.
- [Live Direct Marketing Observability / API Tests API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-observability-api-tests-api/) — The Observability / API Tests API from Live Direct Marketing — 4 operation(s) for observability / api tests.
- [Live Direct Marketing Phantom Browser API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-phantom-browser-api/) — The Phantom Browser API from Live Direct Marketing — 28 operation(s) for phantom browser.
- [Live Direct Marketing Phantom Browser / Download API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-phantom-browser-download-api/) — The Phantom Browser / Download API from Live Direct Marketing — 5 operation(s) for phantom browser / download.
- [Live Direct Marketing Pipeline Events API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-pipeline-events-api/) — The Pipeline Events API from Live Direct Marketing — 9 operation(s) for pipeline events.
- [Live Direct Marketing Pipelines API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-pipelines-api/) — The Pipelines API from Live Direct Marketing — 11 operation(s) for pipelines.
- [Live Direct Marketing Presend API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-presend-api/) — The presend API from Live Direct Marketing — 2 operation(s) for presend.
- [Live Direct Marketing Presend Admin API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-presendadmin-api/) — The PresendAdmin API from Live Direct Marketing — 1 operation(s) for presendadmin.
- [Live Direct Marketing Profi Orders API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-profi-orders-api/) — The Profi Orders API from Live Direct Marketing — 3 operation(s) for profi orders.
- [Live Direct Marketing Project Templates API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-project-templates-api/) — The Project Templates API from Live Direct Marketing — 10 operation(s) for project templates.
- [Live Direct Marketing Prompt Templates API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-prompt-templates-api/) — The Prompt Templates API from Live Direct Marketing — 3 operation(s) for prompt templates.
- [Live Direct Marketing Provider Config API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-provider-config-api/) — The Provider Config API from Live Direct Marketing — 6 operation(s) for provider config.
- [Live Direct Marketing Providers API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-providers-api/) — The providers API from Live Direct Marketing — 2 operation(s) for providers.
- [Live Direct Marketing Public API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-public-api/) — The Public API from Live Direct Marketing — 1 operation(s) for public.
- [Live Direct Marketing Recheck API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-recheck-api/) — The recheck API from Live Direct Marketing — 2 operation(s) for recheck.
- [Live Direct Marketing Reports API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-reports-api/) — The reports API from Live Direct Marketing — 11 operation(s) for reports.
- [Live Direct Marketing RPA API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rpa-api/) — The RPA API from Live Direct Marketing — 7 operation(s) for rpa.
- [Live Direct Marketing RPA service protocol API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rpa-service-protocol-api/) — The RPA service protocol API from Live Direct Marketing — 16 operation(s) for rpa service protocol.
- [Live Direct Marketing Rules / Creative API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rules-creative-api/) — The Rules / Creative API from Live Direct Marketing — 4 operation(s) for rules / creative.
- [Live Direct Marketing Rules / Creative Bootstrap API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rules-creative-bootstrap-api/) — The Rules / Creative Bootstrap API from Live Direct Marketing — 2 operation(s) for rules / creative bootstrap.
- [Live Direct Marketing Rules / Discovery API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rules-discovery-api/) — The Rules / Discovery API from Live Direct Marketing — 2 operation(s) for rules / discovery.
- [Live Direct Marketing Rules / Sub-resource API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rules-sub-resource-api/) — The Rules / Sub-resource API from Live Direct Marketing — 4 operation(s) for rules / sub-resource.
- [Live Direct Marketing RUM API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-rum-api/) — The RUM API from Live Direct Marketing — 1 operation(s) for rum.
- [Live Direct Marketing Saved Views API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-saved-views-api/) — The Saved Views API from Live Direct Marketing — 2 operation(s) for saved views.
- [Live Direct Marketing Screenshots API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-screenshots-api/) — The screenshots API from Live Direct Marketing — 1 operation(s) for screenshots.
- [Live Direct Marketing Search API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-search-api/) — The Search API from Live Direct Marketing — 1 operation(s) for search.
- [Live Direct Marketing Self Control API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-selfcontrol-api/) — The SelfControl API from Live Direct Marketing — 2 operation(s) for selfcontrol.
- [Live Direct Marketing Sender Links API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-sender-links-api/) — The sender-links API from Live Direct Marketing — 5 operation(s) for sender-links.
- [Live Direct Marketing SEO Index API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-seo-index-api/) — The SEO Index API from Live Direct Marketing — 12 operation(s) for seo index.
- [Live Direct Marketing Sequences API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-sequences-api/) — The Sequences API from Live Direct Marketing — 12 operation(s) for sequences.
- [Live Direct Marketing Settings API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-settings-api/) — The Settings API from Live Direct Marketing — 37 operation(s) for settings.
- [Live Direct Marketing Share Links API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-share-links-api/) — The Share Links API from Live Direct Marketing — 2 operation(s) for share links.
- [Live Direct Marketing Share Public API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-share-public-api/) — The Share Public API from Live Direct Marketing — 3 operation(s) for share public.
- [Live Direct Marketing Site Enrichment API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-site-enrichment-api/) — The Site Enrichment API from Live Direct Marketing — 17 operation(s) for site enrichment.
- [Live Direct Marketing Stop List API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-stop-list-api/) — The Stop List API from Live Direct Marketing — 9 operation(s) for stop list.
- [Live Direct Marketing Subscriptions API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-subscriptions-api/) — The subscriptions API from Live Direct Marketing — 3 operation(s) for subscriptions.
- [Live Direct Marketing Subscriptions Admin API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-subscriptionsadmin-api/) — The SubscriptionsAdmin API from Live Direct Marketing — 2 operation(s) for subscriptionsadmin.
- [Live Direct Marketing Support API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-support-api/) — The Support API from Live Direct Marketing — 6 operation(s) for support.
- [Live Direct Marketing Suppression API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-suppression-api/) — The Suppression API from Live Direct Marketing — 6 operation(s) for suppression.
- [Live Direct Marketing System API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-system-api/) — The System API from Live Direct Marketing — 2 operation(s) for system.
- [Live Direct Marketing System Brief Intake API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-systembriefintake-api/) — The SystemBriefIntake API from Live Direct Marketing — 2 operation(s) for systembriefintake.
- [Live Direct Marketing Tags API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tags-api/) — The Tags API from Live Direct Marketing — 8 operation(s) for tags.
- [Live Direct Marketing Tasks API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tasks-api/) — The Tasks API from Live Direct Marketing — 31 operation(s) for tasks.
- [Live Direct Marketing Telegram API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-telegram-api/) — The telegram API from Live Direct Marketing — 3 operation(s) for telegram.
- [Live Direct Marketing Tests API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tests-api/) — The tests API from Live Direct Marketing — 13 operation(s) for tests.
- [Live Direct Marketing Tls Rpt API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tlsrpt-api/) — The TlsRpt API from Live Direct Marketing — 1 operation(s) for tlsrpt.
- [Live Direct Marketing Tracking API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tracking-api/) — The Tracking API from Live Direct Marketing — 14 operation(s) for tracking.
- [Live Direct Marketing Tracking / Bot List API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tracking-bot-list-api/) — The Tracking / Bot List API from Live Direct Marketing — 4 operation(s) for tracking / bot list.
- [Live Direct Marketing Tracking / Domain API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tracking-domain-api/) — The Tracking / Domain API from Live Direct Marketing — 7 operation(s) for tracking / domain.
- [Live Direct Marketing Tracking / Redirect Source API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-tracking-redirect-source-api/) — The Tracking / Redirect Source API from Live Direct Marketing — 3 operation(s) for tracking / redirect source.
- [Live Direct Marketing Unsubscribe API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-unsubscribe-api/) — The Unsubscribe API from Live Direct Marketing — 1 operation(s) for unsubscribe.
- [Live Direct Marketing User Settings API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-user-settings-api/) — The User Settings API from Live Direct Marketing — 2 operation(s) for user settings.
- [Live Direct Marketing Users API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-users-api/) — The Users API from Live Direct Marketing — 12 operation(s) for users.
- [Live Direct Marketing Utils API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-utils-api/) — The Utils API from Live Direct Marketing — 2 operation(s) for utils.
- [Live Direct Marketing Variable Resolver API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-variable-resolver-api/) — The Variable Resolver API from Live Direct Marketing — 2 operation(s) for variable resolver.
- [Live Direct Marketing Webhooks API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-webhooks-api/) — The Webhooks API from Live Direct Marketing — 5 operation(s) for webhooks.
- [Live Direct Marketing Workers API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-workers-api/) — The workers API from Live Direct Marketing — 5 operation(s) for workers.
- [Live Direct Marketing Linked In API](https://apis.io/apis/live-direct-marketing-online/live-direct-marketing-online-linked-in-api/) — The Linked In API from Live Direct Marketing — 9 operation(s) for linked in.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Live Direct Marketing Online Webhooks](https://apis.io/asyncapis/live-direct-marketing-online/live-direct-marketing-online-webhooks/)

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [live-direct-marketing-online-mcp.yml](https://apis.io/servers/live-direct-marketing-online/live-direct-marketing-online-mcp-yml/)
- [Remote endpoint (Streamable HTTP)](https://apis.io/servers/live-direct-marketing-online/remote-endpoint-streamable-http/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Live Direct Marketing Online Agentic Access](https://apis.io/agentic-access/live-direct-marketing-online/live-direct-marketing-online-agentic-access/)

#### Overlays (147)

OpenAPI overlays, including conversational phrasing for each operation.

- [Live Direct Marketing Online A2A Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-a2a-api-phrasing-overlay/)
- [Live Direct Marketing Online Account Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-account-api-phrasing-overlay/)
- [Live Direct Marketing Online Activities Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-activities-api-phrasing-overlay/)
- [Live Direct Marketing Online Admin Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-admin-api-phrasing-overlay/)
- [Live Direct Marketing Online Admin Honeypot Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-admin-honeypot-api-phrasing-overlay/)
- [Live Direct Marketing Online Admin Rpa Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-admin-rpa-api-phrasing-overlay/)
- [Live Direct Marketing Online Agency Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-agency-api-phrasing-overlay/)
- [Live Direct Marketing Online Agent Card Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-agent-card-api-phrasing-overlay/)
- [Live Direct Marketing Online Ai Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-ai-api-phrasing-overlay/)
- [Live Direct Marketing Online Allowlist Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-allowlist-api-phrasing-overlay/)
- [Live Direct Marketing Online Amo Widget Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-amo-widget-api-phrasing-overlay/)
- [Live Direct Marketing Online Api Keys Tenant Scoped Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-api-keys-tenant-scoped-api-phrasing-overlay/)
- [Live Direct Marketing Online Audit Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-audit-api-phrasing-overlay/)
- [Live Direct Marketing Online Auth Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-auth-api-phrasing-overlay/)
- [Live Direct Marketing Online Authentication Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-authentication-api-phrasing-overlay/)
- [Live Direct Marketing Online Best Send Time Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-best-send-time-api-phrasing-overlay/)
- [Live Direct Marketing Online Beta Signups Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-beta-signups-api-phrasing-overlay/)
- [Live Direct Marketing Online Billing Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-billing-api-phrasing-overlay/)
- [Live Direct Marketing Online Branding Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-branding-api-phrasing-overlay/)
- [Live Direct Marketing Online Briefs Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-briefs-api-phrasing-overlay/)
- [Live Direct Marketing Online Browser Queue Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-browser-queue-api-phrasing-overlay/)
- [Live Direct Marketing Online Campaign Groups Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-campaign-groups-api-phrasing-overlay/)
- [Live Direct Marketing Online Campaigns Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-campaigns-api-phrasing-overlay/)
- [Live Direct Marketing Online Canvas Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-canvas-api-phrasing-overlay/)
- [Live Direct Marketing Online Cohort Metrics Api Phrasing Overlay](https://apis.io/overlays/live-direct-marketing-online/live-direct-marketing-online-cohort-metrics-api-phrasing-overlay/)
- …and 122 more published on APIs.io

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Live Direct Marketing Online Authentication](https://apis.io/security/live-direct-marketing-online/live-direct-marketing-online-authentication/)
- [Live Direct Marketing Online Domain Security](https://apis.io/security/live-direct-marketing-online/live-direct-marketing-online-domain-security/)
- [Live Direct Marketing Online Vulnerability Disclosure](https://apis.io/security/live-direct-marketing-online/live-direct-marketing-online-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Live Direct Marketing Online Scopes](https://apis.io/scopes/live-direct-marketing-online/live-direct-marketing-online-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Live Direct Marketing Online Plans Pricing](https://apis.io/plans/live-direct-marketing-online/live-direct-marketing-online-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Live Direct Marketing Online Rate Limits](https://apis.io/rate-limits/live-direct-marketing-online/live-direct-marketing-online-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://live-direct-marketing.online/)
- [Documentation](https://developers.live-direct-marketing.online/)
- [Getting started](https://developers.live-direct-marketing.online/quickstart)
- [API reference](https://developers.live-direct-marketing.online/api-reference)
- [Pricing](https://developers.live-direct-marketing.online/pricing)
- [Sign up](https://developers.live-direct-marketing.online/signup)
- [Support](https://live-direct-marketing.online/contact)
- [Changelog](https://developers.live-direct-marketing.online/changelog)
- [Blog](https://live-direct-marketing.online/blog/)
- [Security](https://developers.live-direct-marketing.online/legal/security)
- [Terms of service](https://live-direct-marketing.online/terms)
- [Privacy policy](https://live-direct-marketing.online/policy)
- [GitHub](https://github.com/live-direct-marketing)

## API Evangelist rating

**Kin Score 68.2** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 49.8 |
| Contract governance | 18.2 |
| Operational transparency | 71.1 |
| Developer ergonomics | 78.6 |
| Access clarity | 76.3 |

**Agent readiness 51.8** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | yes |
| Delegated Identity | — |
| Protected Resource Metadata | documented (partial credit) |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 44.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/live-direct-marketing-online/](https://apis.io/providers/live-direct-marketing-online/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Live Direct Marketing: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/live-direct-marketing-online/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
