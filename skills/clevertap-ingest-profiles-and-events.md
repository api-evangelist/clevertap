---
name: Ingest CleverTap profiles and events
description: >-
  Upload user profiles and behavioral events into CleverTap from an external
  system, batching correctly, honoring the concurrency ceiling, and — critically
  — reading per-record failures out of a HTTP 200 response.
api: openapi/clevertap-profiles-api-openapi.yml
operations:
  - upload
generated: '2026-08-13'
method: generated
source: >-
  openapi/clevertap-profiles-api-openapi.yml, openapi/clevertap-events-api-openapi.yml,
  https://developer.clevertap.com/docs/upload-user-profiles-api,
  https://developer.clevertap.com/docs/upload-events-api,
  https://developer.clevertap.com/docs/api-errors
---

# Ingest CleverTap profiles and events

One endpoint ingests both entity types. Get the identity key and the partial-success
handling right and everything else follows.

## 1. Pick the right host

The base URL is determined by the account's data-center region, not by a path or a
header. Using the wrong host returns **401 Unauthorized**, not a redirect — so a 401
here is as likely to be a region mistake as a credential mistake.

| Region | Host |
|---|---|
| Europe (default) | `https://api.clevertap.com` |
| India | `https://in1.api.clevertap.com` |
| Singapore | `https://sg1.api.clevertap.com` |
| United States | `https://us1.api.clevertap.com` |
| Indonesia | `https://aps3.api.clevertap.com` |
| Middle East (UAE) | `https://mec1.api.clevertap.com` |

## 2. Authenticate

Every request carries three headers:

```
X-CleverTap-Account-Id: <account id>
X-CleverTap-Passcode: <passcode>
Content-Type: application/json
```

These are static, unscoped and non-expiring. Treat them as full account authority and
never place them in a client-side context.

## 3. Call `upload`

`POST /1/upload` — operationId **`upload`**.

The body is `{"d": [ ... ]}` with at most **1000 records** per call. Each record
declares its own `type`:

```json
{
  "d": [
    {
      "type": "profile",
      "identity": "user-1234",
      "profileData": {"Name": "Jane Doe", "Customer Type": "Silver"}
    },
    {
      "type": "event",
      "identity": "user-1234",
      "evtName": "Product Viewed",
      "evtData": {"Product ID": "SKU-99", "Price": 4200},
      "ts": 1786634590
    }
  ]
}
```

Rules that cause most failures:

- Every record needs an identity key — one of `identity`, `objectId`, `FBID` or
  `GPID`. A record with none fails with code **523**.
- `type` must be exactly `profile` or `event`. Anything else fails with **524**.
- `ts` is **Unix epoch seconds**, not milliseconds and not ISO-8601. Wrong format
  fails with **525**.
- `evtName` is mandatory on events (**509** if missing) and must not be a reserved
  system event (**513**).

## 4. Read the partial-success response — this is the step that gets skipped

`upload` returns **HTTP 200 even when records failed**:

```json
{"status": "success", "processed": 998, "unprocessed": [{"status":"fail","code":515,"error":"Email invalid"}]}
```

Never treat the 200 as success. Compare `processed` against the number of records you
sent, and iterate `unprocessed[]`. Each entry carries a CleverTap numeric code from
`errors/clevertap-error-codes.yml` — for example 514 gender invalid, 515 email invalid,
516 phone invalid, 520 age invalid, 526 objectId invalid.

## 5. Concurrency, not rate

CleverTap does **not** throttle on a time window. It caps **parallel in-flight
requests per account**: 15 concurrent for the upload endpoints, 3 for everything
else. Exceeding it returns **429 "Too many concurrent requests"** with no
`Retry-After` and no `X-RateLimit-*` headers. Cap your worker pool at 15 rather than
pacing by requests-per-second.

## 6. There is no idempotency key

CleverTap documents no idempotency header and no request-deduplication contract. A
retried upload re-applies. Profile records converge because they are keyed on
identity, but **events do not** — a retried event batch double-counts. Before
retrying a failed upload, retry only the records in `unprocessed[]`, never the whole
batch.
