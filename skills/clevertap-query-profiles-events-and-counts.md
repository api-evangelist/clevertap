---
name: Query CleverTap profiles, events and counts
description: >-
  Read data back out of CleverTap — look up a single profile, page through a
  profile or event query with the two-step cursor flow, and pull real-time event
  and profile counts.
api: openapi/clevertap-profiles-api-openapi.yml
operations:
  - getProfile
  - queryProfiles
  - queryEvents
  - getEventCounts
  - getProfileCounts
  - disassociateProfile
generated: '2026-08-13'
method: generated
source: >-
  openapi/clevertap-profiles-api-openapi.yml, openapi/clevertap-events-api-openapi.yml,
  openapi/clevertap-reports-api-openapi.yml,
  https://developer.clevertap.com/docs/get-user-profiles-api,
  https://developer.clevertap.com/docs/get-events-api,
  https://developer.clevertap.com/docs/authentication
---

# Query CleverTap profiles, events and counts

Reads on this API come in two shapes: a direct lookup, and a two-step cursor query.
Getting the cursor flow right is the whole job.

## 1. Direct profile lookup

`GET /1/profile.json` — operationId **`getProfile`**.

Pass exactly one of `identity` or `objectId` as a query parameter:

```
GET /1/profile.json?identity=user-1234
```

This is the only true GET-with-params read on the API.

## 2. The two-step cursor query

Bulk reads are POST-then-GET. The query language is CleverTap Query Language (CQL),
which is why the query is a body rather than query parameters.

**Step 1 — get a cursor.** POST the query:

- `POST /1/profiles.json` — operationId **`queryProfiles`**
- `POST /1/events.json` — operationId **`queryEvents`**

The response carries a `cursor`.

**Step 2 — fetch pages.** GET the *same* path with the cursor:

```
GET /1/events.json?cursor=<cursor>
```

Each page response carries `next_cursor`. Loop, feeding `next_cursor` back into the
same GET, until it is absent. `batch_size` controls page size.

Do not try to page by offset or by date range — cursor is the only pagination
mechanism, and cursors are opaque and single-use in sequence.

## 3. Counts

- `POST /1/counts/event.json` — operationId **`getEventCounts`**
- `POST /1/counts/profile.json` — operationId **`getProfileCounts`**

Both take a CQL body describing the event or profile property and the duration. These
are the cheap way to answer "how many" without paging the full result set — prefer
them over counting pages.

## 4. Deleting a profile

`POST /1/disassociate` — operationId **`disassociateProfile`**.

This detaches identity from a profile. It is destructive and not reversible, and it is
subject to data-subject-request handling on the customer's side. Escalate to a human
before calling it; never call it speculatively as part of a retry.

## 5. Limits that bite on reads

- Every read endpoint here allows **3 concurrent requests per account**. Paging loops
  are the easiest way to trip 429; run one cursor loop at a time.
- There are no `X-RateLimit-*` headers and no `Retry-After`. On 429, reduce
  parallelism — waiting does not help if you are still over the concurrency ceiling.
- Responses are plain JSON, not RFC 9457 problem+json. See
  `errors/clevertap-error-codes.yml`.

## 6. Optional payload encryption

If the account has HPKE enabled, both the cursor request and the page fetch are
encrypted binary payloads and the response must be decrypted with the customer's
private key. See <https://developer.clevertap.com/docs/api-encryption>.
