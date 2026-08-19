---
name: Create a CleverTap campaign and report on it
description: >-
  Estimate, create, monitor and stop a CleverTap campaign across push, email,
  SMS, web, WhatsApp, webhook or notification-inbox channels, using the
  estimate-then-send safety pattern.
api: openapi/clevertap-campaigns-api-openapi.yml
operations:
  - createCampaign
  - getCampaignResult
  - stopCampaign
generated: '2026-08-13'
method: generated
source: >-
  openapi/clevertap-campaigns-api-openapi.yml,
  https://developer.clevertap.com/docs/create-campaign-api,
  https://developer.clevertap.com/docs/get-campaign-report-api,
  https://developer.clevertap.com/docs/stop-campaign-api
---

# Create a CleverTap campaign and report on it

Campaign creation is the highest-consequence operation on this API: it sends real
messages to real people and it is **not reversible and not idempotent**. Follow the
estimate-first pattern.

## 1. Estimate before you send

`POST /1/targets/create.json` — operationId **`createCampaign`** — accepts
`estimate_only: true`. Send the exact body you intend to send for real, with that flag
set, and read back the audience size. Do this every time. There is no dry-run mode
other than this flag, and no way to recall a campaign once it has gone out.

```json
{
  "name": "Cart abandonment nudge",
  "target_mode": "push",
  "estimate_only": true,
  "where": { "event_name": "Charged", "from": 20260801, "to": 20260813 },
  "content": { "title": "Still thinking it over?", "body": "Your cart is waiting." },
  "when": "now",
  "respect_frequency_caps": true
}
```

`target_mode` is one of `push`, `email`, `sms`, `webpush`, `whatsapp`, `webhook`,
`notificationinbox`. `name`, `target_mode`, `content` and `when` are all required.

## 2. Send

Re-issue the same call with `estimate_only` removed (or use `draft: true` to stage it
for a human to release from the dashboard). Keep `respect_frequency_caps: true` unless
you have an explicit instruction not to — it is the only guard against over-messaging.

The response returns a **`req_id`**. Hold on to it; it is the only handle to the
campaign's report.

There is no idempotency key on this endpoint. A retry after a timeout may create a
**second campaign** and send the messages twice. If a create call times out, do not
retry blindly — query the campaign list or the dashboard first.

## 3. Report

`GET /1/targets/result.json?req_id=<req_id>` — operationId **`getCampaignResult`**.

`req_id` is a required query parameter. Poll it for delivery and engagement counts.
Concurrency ceiling on this endpoint is **3**.

## 4. Stop

`POST /1/targets/stop.json` — operationId **`stopCampaign`** — with `{"id": "<campaign id>"}`.

This only stops a **scheduled or recurring** campaign that has not yet been delivered.
It cannot recall messages already sent. Treat it as safety-critical: escalate to a
human before calling it, since stopping a live recurring campaign is an operationally
visible action with no undo.

## 5. Errors and limits

- **429 "Too many concurrent requests"** — campaign endpoints allow only **3**
  concurrent requests per account. There is no `Retry-After` header; back off yourself.
- **401** — check the regional host as well as the credentials; the wrong region
  presents as an auth failure.
- Full status and code table: `errors/clevertap-error-codes.yml`.
