# CleverTap (clevertap)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

CleverTap is a customer engagement and retention platform that helps businesses understand user behavior, segment audiences, and deliver personalized experiences across mobile push, email, SMS, in-app, web push, and WhatsApp channels. CleverTap exposes a comprehensive REST API surface covering profiles, events, campaigns, real-time analytics, catalogs, feature flags, and more, authenticated via account ID and passcode headers.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/clevertap/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/clevertap/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Audiences
- Customer Engagement
- Customer Retention
- Marketing Automation
- Mobile Engagement
- Push Notifications
- User Behavior

## Timestamps

- **Created:** 2024-11-14
- **Modified:** 2026-04-26

## APIs

### CleverTap Profile API

Upload, retrieve, update, and delete user profiles in CleverTap with identity, demographic, and custom property data.

- **Human URL:** [https://developer.clevertap.com/docs/profile-api](https://developer.clevertap.com/docs/profile-api)

#### Tags

- Profiles
- User Data

#### Properties

- [Documentation](https://developer.clevertap.com/docs/profile-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Event API

Record user events with arbitrary properties for behavioral segmentation, funnels, and triggered messaging.

- **Human URL:** [https://developer.clevertap.com/docs/event-api](https://developer.clevertap.com/docs/event-api)

#### Tags

- Events
- Tracking

#### Properties

- [Documentation](https://developer.clevertap.com/docs/event-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Campaign API

Programmatically create and manage push, email, SMS, web, and in-app campaigns and retrieve message status reports.

- **Human URL:** [https://developer.clevertap.com/docs/create-a-campaign-api](https://developer.clevertap.com/docs/create-a-campaign-api)

#### Tags

- Campaigns
- Messaging

#### Properties

- [Documentation](https://developer.clevertap.com/docs/create-a-campaign-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Bulletins API

Raise a Bulletin in CleverTap when a business event is triggered, used to drive real-time campaign delivery from external systems.

- **Human URL:** [https://developer.clevertap.com/docs/bulletins-api](https://developer.clevertap.com/docs/bulletins-api)

#### Tags

- Bulletins
- Triggers

#### Properties

- [Documentation](https://developer.clevertap.com/docs/bulletins-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Catalog API

Manage product catalog data feeding personalization, recommendations, and product-aware messaging.

- **Human URL:** [https://developer.clevertap.com/docs/catalog-api](https://developer.clevertap.com/docs/catalog-api)

#### Tags

- Catalog
- Product Data

#### Properties

- [Documentation](https://developer.clevertap.com/docs/catalog-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Custom List API

Create and update custom lists used as audience segments in campaigns and journeys.

- **Human URL:** [https://developer.clevertap.com/docs/custom-list-api](https://developer.clevertap.com/docs/custom-list-api)

#### Tags

- Audiences
- Lists

#### Properties

- [Documentation](https://developer.clevertap.com/docs/custom-list-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Remote Config API

Manage feature flags and remote configuration variables delivered to mobile apps and websites.

- **Human URL:** [https://developer.clevertap.com/docs/remote-config-api](https://developer.clevertap.com/docs/remote-config-api)

#### Tags

- Feature Flags
- Remote Config

#### Properties

- [Documentation](https://developer.clevertap.com/docs/remote-config-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CleverTap Real-Time Counts API

Query real-time counts and trends of events, profiles, and segments.

- **Human URL:** [https://developer.clevertap.com/docs/real-time-counts-api](https://developer.clevertap.com/docs/real-time-counts-api)

#### Tags

- Analytics
- Counts

#### Properties

- [Documentation](https://developer.clevertap.com/docs/real-time-counts-api)
- [Postman Collection](collections/clevertap.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/clevertap.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/CleverTap)
- [LinkedIn](https://www.linkedin.com/company/clevertap)
- [Website](https://clevertap.com/)
- [Developer  Portal](https://developer.clevertap.com/)
- [Documentation](https://developer.clevertap.com/docs)
- [Authentication](https://developer.clevertap.com/docs/api-authentication)
- [Status Page](https://status.clevertap.com/)
- [Pricing](https://clevertap.com/pricing/)
- [Privacy Policy](https://clevertap.com/privacy-policy/)
- [Terms of Service](https://clevertap.com/terms-of-service/)
- [JSON-LD](json-ld/clevertap-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Spectral Rules](rules/clevertap-rules.yml) — [Spectral](https://docs.stoplight.io/docs/spectral)
- [L L Ms Txt](https://developer.clevertap.com/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kinlane@gmail.com
