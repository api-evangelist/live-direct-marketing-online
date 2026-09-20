---
name: live-direct-marketing-online-inbox-placement-test
description: Run an inbox-placement test against the Inbox Check API — check quota, create the test, send to the seed mailboxes, poll results, re-poll or schedule a same-message recheck, and read the report.
api: Inbox Check API
base_url: https://check.live-direct-marketing.online
generated: '2026-09-19'
method: generated
source: openapi/live-direct-marketing-online-inbox-check-openapi.json + https://check.live-direct-marketing.online/docs (all operationIds verified in the contract)
operations:
  - V1MeController_me
  - V1ProvidersController_list
  - V1TestsController_create
  - V1TestsController_createAuto
  - V1TestsController_get
  - V1TestsController_repoll
  - V1TestsController_scheduleDeferredRecheck
  - V1TestsController_deferredRecheckStatus
  - V1TestsController_list
  - V1TestsController_remove
---

# Run an inbox-placement test

Use this when you need to know where an email actually lands — Inbox, Spam, Promotions or Not
received — across Gmail, Outlook, Yahoo, iCloud, AOL, GMX, Web.de, T-Online, Mail.ru and Yandex,
before a campaign is scaled. The same tools exist on the remote MCP server
(`https://check.live-direct-marketing.online/mcp`) under the names `me_get`, `providers_list`,
`tests_create`, `tests_get`, `tests_repoll`, `tests_recheck`.

## Credential

`Authorization: Bearer icp_live_<key>` on every call. Keys are self-issued at
`https://check.live-direct-marketing.online/account` (basic tier: 100 tests/day, 1,000/month, no
screenshots) and are shown once. There is no test-mode key; every test consumes real quota.

## Steps

1. **Check quota first.** `V1MeController_me` (`GET /api/v1/me`) returns `tier`, `features`,
   `allowed_providers` and `usage.daily_used / daily_limit / monthly_used / monthly_limit`. If the
   daily or monthly counter is at its limit, stop — the create call will answer
   `402 quota_exceeded`, which the provider says is "a signal to upgrade your tier, not to retry".
2. **Pick providers.** `V1ProvidersController_list` (`GET /api/v1/providers`) lists every provider
   and marks which ones this key may use, with a reason for the ones it cannot. Only request
   providers in the allowlist; otherwise you get `400 providers_not_allowed`.
3. **Create the test.** Manual mode — `V1TestsController_create` (`POST /api/v1/tests`) with
   `{ "providers": [...], "recipient_email"?: "...", "meta"?: {...}, "screenshots"?: bool }`.
   Auto mode — `V1TestsController_createAuto` (`POST /api/v1/tests/auto`) with a `recipient_email`;
   the service classifies the provider via MX and picks ONE matching seed. Both answer `202` with
   `token`, `send_to[]` (one seed address per provider, plus-addressed with the token),
   `results_url`, `expires_at` and the remaining quota. One quota unit is consumed on success.
4. **Send the email yourself** from the real sending system to every address in `send_to[]`. The
   API never sends mail; it only receives.
5. **Poll.** `V1TestsController_get` (`GET /api/v1/tests/{token}`) until `status` is `done` or
   `expired` (tests complete within about 15 minutes; unreceived seeds are reported as Not
   received). The snapshot carries per-seed `placement`, `spf/dkim/dmarc`, `screenshot_url` when
   enabled, an aggregate `summary`, `verdict` and `recommendations`. Pass `?format=pdf` (requires
   the `reports:pdf` scope) for a PDF report.
6. **If delivery is slow,** `V1TestsController_repoll` (`POST /api/v1/tests/{token}/repoll`) forces
   an IMAP fetch on every seed. 30-second cooldown per token; no quota consumed.
7. **To see whether placement changes later,** `V1TestsController_scheduleDeferredRecheck`
   (`POST /api/v1/tests/{token}/recheck`, `delay_hours` 1–168, default 24) schedules a re-scan of
   the same message — no new email, no quota — and `V1TestsController_deferredRecheckStatus`
   (`GET /api/v1/tests/{token}/recheck-status`) returns both snapshots and the transition matrix.
8. **Page history** with `V1TestsController_list` (`GET /api/v1/tests?cursor=<created_at>`), newest
   first; the response carries `next_cursor`.

## Rules

- `V1TestsController_remove` (`DELETE /api/v1/tests/{token}`) is **irreversible** — it removes the
  results and screenshot jobs. Do not call it to "reset" a test; create a new one.
- Test records are retained 7 days and then deleted; fetch what you need before `expires_at`.
- Errors arrive as RFC 9457 `application/problem+json` with a `code` member
  (`auth_required`, `invalid_api_key`, `quota_exceeded`, `providers_not_allowed`,
  `no_seeds_for_provider`, `test_not_found`, `service_overloaded`). `503 service_overloaded` means
  the seed pool is exhausted — retry in a few minutes; `402` and `401` mean do not retry.
- No `X-RateLimit-*` or `Retry-After` headers are sent; read quota from step 1.
- A green result on one provider is not a deliverability verdict: the provider notes Gmail is the
  most lenient and a test with fewer than four providers is indicative only for those tested.
