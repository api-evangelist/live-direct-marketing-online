---
name: live-direct-marketing-online-domain-monitoring
description: Put a sending domain under continuous SPF / DMARC / MX / blocklist / TLS monitoring with the Inbox Check API, read its history, pause and resume it, and configure how alerts are delivered.
api: Inbox Check API
base_url: https://check.live-direct-marketing.online
generated: '2026-09-19'
method: generated
source: openapi/live-direct-marketing-online-inbox-check-openapi.json + https://check.live-direct-marketing.online/docs/mcp (all operationIds verified in the contract)
operations:
  - V1MonitoringController_list
  - V1MonitoringController_add
  - V1MonitoringController_run
  - V1MonitoringController_latest
  - V1MonitoringController_listChecks
  - V1MonitoringController_pause
  - V1MonitoringController_resume
  - V1MonitoringController_getSettings
  - V1MonitoringController_updateSettings
  - V1MonitoringController_remove
---

# Monitor a sending domain

Use this to watch a domain's mail authentication and reputation over time rather than testing a
single message. MCP tool names: `monitor_domain_list`, `monitor_domain_create`, `monitor_domain_run`,
`monitor_domain_latest`, `monitor_domain_checks`, `monitor_domain_pause`, `monitor_domain_resume`,
`monitor_domain_delete`, `monitor_settings_get`, `monitor_settings_update`.

## Credential

A **user-bound** `icp_live_*` key from a verified account. Read calls need `monitoring:read`
(default); every mutation needs `monitoring:write`, which the owner must tick when creating the key
("Allow this key to add, pause, resume and delete my monitored domains"). Unbound keys receive 403.

## Steps

1. **See what is already monitored.** `V1MonitoringController_list`
   (`GET /api/v1/monitoring/domains`) returns the domains and the per-user active-domain limit
   (100 per account, shared with the website and Telegram).
2. **Add the domain.** `V1MonitoringController_add` (`POST /api/v1/monitoring/domains`) with
   `{ "domain": "example.com", "enabledChecks"?: ["spf","dmarc","mx","blocklist","tls"] }`
   (`domain` 3–253 chars). Keep the returned `id`.
3. **Run a check now** instead of waiting for the schedule: `V1MonitoringController_run`
   (`POST /api/v1/monitoring/domains/{id}/run`).
4. **Read results.** `V1MonitoringController_latest` (`GET .../{id}/latest`) for the most recent
   check; `V1MonitoringController_listChecks` (`GET .../{id}/checks`) for history, newest first.
5. **Configure alerts.** `V1MonitoringController_getSettings` /
   `V1MonitoringController_updateSettings` (`GET|PATCH /api/v1/monitoring/settings`) with any of
   `emailEnabled`, `webhookUrl` (uri, ≤ 2048), `webhookSecret` (≤ 256), `alertOnInfo`,
   `alertOnWarn`, `alertOnCrit`, `digestFrequency` (`off|weekly|monthly`), `telegramEnabled`.
6. **Pause rather than delete** when a domain is temporarily out of use:
   `V1MonitoringController_pause` suspends scheduled checks and keeps history;
   `V1MonitoringController_resume` re-enables them.

## Rules

- `V1MonitoringController_remove` (`DELETE /api/v1/monitoring/domains/{id}`) **deletes the domain
  and its entire check history and is irreversible**. Prefer pause. Ask the human before deleting.
- Monitoring settings are per key owner, not per domain.
- The webhook alert payload and its signing are not documented; treat `webhookSecret` as a shared
  secret you verify on your side and confirm the shape from a first delivery.
- Errors are RFC 9457 `application/problem+json`; 401 `auth_required` / `invalid_api_key` and 403
  (missing `monitoring:write` or key not user-bound) are not retryable.
