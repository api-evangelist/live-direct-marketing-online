---
name: live-direct-marketing-online-agent-bootstrap
description: Bootstrap an LDM workspace as an agent — read the terms, register with channel=mcp to receive a PENDING-account ldm_* key, verify it, read balance and public pricing, load the agent guide, and rehearse a campaign with the send-readiness dry-run before anything is sent.
api: LDM v3 API
base_url: https://api.live-direct-marketing.online
generated: '2026-09-19'
method: generated
source: openapi/live-direct-marketing-online-ldm-v3-openapi.json + https://developers.live-direct-marketing.online/quickstart, /api-registration, /limits (all operationIds verified in the contract)
operations:
  - LegalController_getTerms
  - AuthController_register
  - AuthController_getMe
  - BillingController_getBalance
  - PublicPricingController_pricing
  - AgentGuideController_guide
  - CampaignsController_sendReadiness
---

# Bootstrap an LDM workspace as an agent

LDM is built to be operated by agents: the same `/api/*` routes serve the web UI and MCP/A2A
clients, and a key can be minted without a human. Over MCP the first three steps are the anonymous
tools `ldm_terms` → `ldm_register` (then reconnect with the key). This skill is the REST equivalent.

## Steps

1. **Read the agreement and show it to the user.** `LegalController_getTerms`
   (`GET /api/legal/terms`, public; default locale is ru — request `?locale=en`). Registration
   requires `termsAccepted: true`, so the human must actually see it.
2. **Register.** `AuthController_register` (`POST /api/auth/register`) with
   `{ "email", "termsAccepted": true, "channel": "mcp", "website"?: "https://<company site on the same domain>", "org"?, "use_case"?, "firstName"? }`.
   For `channel` `mcp|a2a|form` the response is flat: `api_key` (`ldm_...`), `scope[]`, `quota`,
   `tenant`, `pending: true`. The account is **PENDING** until the confirmation email (valid 48 h)
   is clicked; pass `website` on the email's own domain to qualify for automatic activation,
   otherwise the signup goes to a questionnaire and admin approval. Rate limit: 3 signups per hour
   per IP (`429 {error: rate_limited}`).
3. **Verify the key.** `AuthController_getMe` (`GET /api/auth/me`) with
   `Authorization: Bearer ldm_...`. Reads work immediately on a PENDING account.
4. **Know what you can and cannot do.** The auto-issued key carries `SAFE_AGENT_SCOPES` — read-all
   plus safe drafts — and explicitly **not** `email:send` or `mailing:write`; the owner widens the
   key in CRM Settings → API Keys after activation. Self-signup workspaces have a 50 MB database
   quota; over it, writes return 403 while reads and DELETE keep working.
5. **Read money before spending it.** `PublicPricingController_pricing`
   (`GET /api/public/pricing`, no auth) for list rates and `BillingController_getBalance`
   (`GET /api/billing/balance`) for the effective rates, balance and `topUpUrl`. Paid operations
   answer `402 {code: insufficient_balance, required, balance, topUpUrl}` and execute nothing
   partially. The beta runs in `payment.mode: demo` with a $50 signup credit and manual top-ups.
6. **Load the map.** `AgentGuideController_guide` (`GET /api/v1/agent-guide`) returns the 33
   capability domains and the provider's recommended eight-step outreach flow (verify addresses
   first; test placement before scaling; send `limit=1` and measure). Every MCP/A2A response also
   carries an `_expert` block; send `X-LDM-Guidance: off` to suppress it.
7. **Rehearse before sending.** For any campaign, `CampaignsController_sendReadiness`
   (`GET /api/campaigns/{id}/send-readiness`) dry-runs every send gate — status, circuit breaker,
   send window, sender pool, routing, inbox-check, due READY rows — and sends nothing. Read
   `effective.sendWindow.windowOpen` / `nextOpenAt` and `operationalState` before any send call.

## Rules

- Tenant-scoped calls take `X-Tenant-Id: <uuid>`; the key is bound to its home tenant, so omit
  it unless pivoting an agency tenant.
- Campaign launch requires explicit human confirmation; suppression and stop-lists run before every
  send; unsubscribes are honoured permanently — the platform states it "will not send what must not
  be sent, even if instructed to".
- `PATCH /api/campaigns/{id}/recipients/{rid}/manual` is human-only: agents get `403 human_only`.
- Only `POST /api/campaigns/{id}/test-task` declares an `idempotency-key` header; assume other
  writes are not replay-safe and never blind-retry a send.
- Errors are `{ statusCode, message }` (validation returns `message[]`); 401 is deliberately
  generic. No `X-RateLimit-*` headers are sent.
