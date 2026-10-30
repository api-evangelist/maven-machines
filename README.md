# Maven Machines

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

Maven Machines (branded "Maven") is a Pittsburgh, Pennsylvania software company that builds a cloud platform for automating the planning and execution of daily trucking operations. The product suite spans route planning and optimization, dispatch execution, driver workflow, ELD / hours-of-service compliance, telematics and fleet management, delivered through a web portal for planners and dispatchers and an Android driver application. Maven publishes a public developer hub at maven-machines.readme.io covering fifteen separate OpenAPI definitions against a single production base URL, https://integrations.mavenmachines.com, secured with an `apiKey` request header. The integration model is TMS-to-Maven — master data (users, vehicles, trailers, company locations), transactional data (shipments, P&D manifests, linehaul manifests and trips, truckload trips and stops) flows in, and business activity flows back out through a polled `GET /return-events` queue and an event-sourced manifest/movement commands API. Maven also operates per-customer integration middleware services on <customer>.middleware.mavenmachines.com, several of which publish their own Swagger/OpenAPI documents publicly.

**Areas:** Transportation · Logistics · Trucking · Fleet Management · Telematics · ELD · Route Optimization · Dispatch · Supply Chain · Freight

## Maven Machines on APIs.io

Everything profiled for Maven Machines is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/maven-machines/](https://apis.io/providers/maven-machines/)** — or go straight to one of the APIs or properties below.

### APIs (28)

- [Maven Machines Bulk Shipments API](https://apis.io/apis/maven-machines/maven-machines-bulk-shipments-api/) — The bulk-shipments API from Maven Machines — 1 operation(s) for bulk-shipments.
- [Maven Machines Company Locations API](https://apis.io/apis/maven-machines/maven-machines-company-locations-api/) — The company-locations API from Maven Machines — 1 operation(s) for company-locations.
- [Maven Machines Customers API](https://apis.io/apis/maven-machines/maven-machines-customers-api/) — The Customers API from Maven Machines — 1 operation(s) for customers.
- [Maven Machines Eld API](https://apis.io/apis/maven-machines/maven-machines-eld-api/) — The Eld API from Maven Machines — 3 operation(s) for eld.
- [Maven Machines Events API](https://apis.io/apis/maven-machines/maven-machines-events-api/) — The Events API from Maven Machines — 1 operation(s) for events.
- [Maven Machines Forms API](https://apis.io/apis/maven-machines/maven-machines-forms-api/) — The forms API from Maven Machines — 2 operation(s) for forms.
- [Maven Machines Health API](https://apis.io/apis/maven-machines/maven-machines-health-api/) — The health API from Maven Machines — 1 operation(s) for health.
- [Maven Machines Linehaul API](https://apis.io/apis/maven-machines/maven-machines-linehaul-api/) — The Linehaul API from Maven Machines — 2 operation(s) for linehaul.
- [Maven Machines Locations API](https://apis.io/apis/maven-machines/maven-machines-locations-api/) — The Locations API from Maven Machines — 2 operation(s) for locations.
- [Maven Machines Manifest Number API](https://apis.io/apis/maven-machines/maven-machines-manifestnumber-api/) — The ManifestNumber API from Maven Machines — 1 operation(s) for manifestnumber.
- [Maven Machines Manifests API](https://apis.io/apis/maven-machines/maven-machines-manifests-api/) — The manifests API from Maven Machines — 5 operation(s) for manifests.
- [Maven Machines Marketapps API](https://apis.io/apis/maven-machines/maven-machines-marketapps-api/) — The marketapps API from Maven Machines — 1 operation(s) for marketapps.
- [Maven Machines Messages API](https://apis.io/apis/maven-machines/maven-machines-messages-api/) — The messages API from Maven Machines — 1 operation(s) for messages.
- [Maven Machines Orders API](https://apis.io/apis/maven-machines/maven-machines-orders-api/) — The orders API from Maven Machines — 3 operation(s) for orders.
- [Maven Machines Pickup Requests API](https://apis.io/apis/maven-machines/maven-machines-pickuprequests-api/) — The PickupRequests API from Maven Machines — 1 operation(s) for pickuprequests.
- [Maven Machines Product Eligibility API](https://apis.io/apis/maven-machines/maven-machines-product-eligibility-api/) — The product-eligibility API from Maven Machines — 1 operation(s) for product-eligibility.
- [Maven Machines Reddy Ice API](https://apis.io/apis/maven-machines/maven-machines-reddy-ice-api/) — The reddy-ice API from Maven Machines — 1 operation(s) for reddy-ice.
- [Maven Machines Reports API](https://apis.io/apis/maven-machines/maven-machines-reports-api/) — The reports API from Maven Machines — 1 operation(s) for reports.
- [Maven Machines Return Events API](https://apis.io/apis/maven-machines/maven-machines-return-events-api/) — The Return Events API from Maven Machines — 1 operation(s) for return events.
- [Maven Machines Servicetechs API](https://apis.io/apis/maven-machines/maven-machines-servicetechs-api/) — The servicetechs API from Maven Machines — 3 operation(s) for servicetechs.
- [Maven Machines Shipment API](https://apis.io/apis/maven-machines/maven-machines-shipment-api/) — The shipment API from Maven Machines — 3 operation(s) for shipment.
- [Maven Machines Shipment Locations API](https://apis.io/apis/maven-machines/maven-machines-shipment-locations-api/) — The shipment-locations API from Maven Machines — 1 operation(s) for shipment-locations.
- [Maven Machines Smart API](https://apis.io/apis/maven-machines/maven-machines-smart-api/) — The smart API from Maven Machines — 2 operation(s) for smart.
- [Maven Machines Trailers API](https://apis.io/apis/maven-machines/maven-machines-trailers-api/) — The Trailers API from Maven Machines — 3 operation(s) for trailers.
- [Maven Machines Truckload API](https://apis.io/apis/maven-machines/maven-machines-truckload-api/) — The truckload API from Maven Machines — 3 operation(s) for truckload.
- [Maven Machines Users API](https://apis.io/apis/maven-machines/maven-machines-users-api/) — The users API from Maven Machines — 1 operation(s) for users.
- [Maven Machines Vehicles API](https://apis.io/apis/maven-machines/maven-machines-vehicles-api/) — The Vehicles API from Maven Machines — 3 operation(s) for vehicles.
- [Maven Machines Route Plans API](https://apis.io/apis/maven-machines/maven-machines-route-plans-api/) — The Route Plans API from Maven Machines — 1 operation(s) for route plans.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Maven Machines Return Events](https://apis.io/asyncapis/maven-machines/maven-machines-return-events/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [maven-machines-mcp.yml](https://apis.io/servers/maven-machines/maven-machines-mcp-yml/)

#### Overlays (22)

OpenAPI overlays, including conversational phrasing for each operation.

- [_Index](https://apis.io/overlays/maven-machines/_index/)
- [Maven Machines Aaa Cooper Middleware Overlay](https://apis.io/overlays/maven-machines/maven-machines-aaa-cooper-middleware-overlay/)
- [Maven Machines Assets Overlay](https://apis.io/overlays/maven-machines/maven-machines-assets-overlay/)
- [Maven Machines Averitt Middleware Overlay](https://apis.io/overlays/maven-machines/maven-machines-averitt-middleware-overlay/)
- [Maven Machines Bozzutos Middleware Overlay](https://apis.io/overlays/maven-machines/maven-machines-bozzutos-middleware-overlay/)
- [Maven Machines Company Locations Overlay](https://apis.io/overlays/maven-machines/maven-machines-company-locations-overlay/)
- [Maven Machines Eld Hos Overlay](https://apis.io/overlays/maven-machines/maven-machines-eld-hos-overlay/)
- [Maven Machines Linehaul Overlay](https://apis.io/overlays/maven-machines/maven-machines-linehaul-overlay/)
- [Maven Machines Manifest Commands Overlay](https://apis.io/overlays/maven-machines/maven-machines-manifest-commands-overlay/)
- [Maven Machines Market Apps Overlay](https://apis.io/overlays/maven-machines/maven-machines-market-apps-overlay/)
- [Maven Machines Messages Overlay](https://apis.io/overlays/maven-machines/maven-machines-messages-overlay/)
- [Maven Machines Planning And Dispatch Overlay](https://apis.io/overlays/maven-machines/maven-machines-planning-and-dispatch-overlay/)
- [Maven Machines Reddy Ice Middleware Overlay](https://apis.io/overlays/maven-machines/maven-machines-reddy-ice-middleware-overlay/)
- [Maven Machines Reports Overlay](https://apis.io/overlays/maven-machines/maven-machines-reports-overlay/)
- [Maven Machines Rest Service Manual Overlay](https://apis.io/overlays/maven-machines/maven-machines-rest-service-manual-overlay/)
- [Maven Machines Roy Miller Middleware Overlay](https://apis.io/overlays/maven-machines/maven-machines-roy-miller-middleware-overlay/)
- [Maven Machines Shipment Locations Overlay](https://apis.io/overlays/maven-machines/maven-machines-shipment-locations-overlay/)
- [Maven Machines Shipments Overlay](https://apis.io/overlays/maven-machines/maven-machines-shipments-overlay/)
- [Maven Machines Smart Overlay](https://apis.io/overlays/maven-machines/maven-machines-smart-overlay/)
- [Maven Machines Triple S Steel Middleware Overlay](https://apis.io/overlays/maven-machines/maven-machines-triple-s-steel-middleware-overlay/)
- [Maven Machines Users Overlay](https://apis.io/overlays/maven-machines/maven-machines-users-overlay/)
- [Maven Machines Workflow Overlay](https://apis.io/overlays/maven-machines/maven-machines-workflow-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Maven Machines Authentication](https://apis.io/security/maven-machines/maven-machines-authentication/)
- [Maven Machines Domain Security](https://apis.io/security/maven-machines/maven-machines-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Maven Machines Plans Pricing](https://apis.io/plans/maven-machines/maven-machines-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Maven Machines Rate Limits](https://apis.io/rate-limits/maven-machines/maven-machines-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://mavenmachines.com/)
- [Documentation](https://maven-machines.readme.io/)
- [Getting started](https://maven-machines.readme.io/docs/basic-concepts)
- [API reference](https://maven-machines.readme.io/reference/post-shipment)
- [Sign up](https://accounts.mavenmachines.com/)
- [Support](https://help.mavenmachines.com/)
- [Blog](https://mavenmachines.com/blog/)
- [Privacy policy](https://mavenmachines.com/privacy-policy/)
- [GitHub](https://github.com/Maven-Machines)
- [Status](https://mavenmachines.statuspage.io/)

## API Evangelist rating

**Kin Score 41.1** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 59.6 |
| Contract governance | 4.5 |
| Operational transparency | 18.4 |
| Developer ergonomics | 47.0 |
| Access clarity | 23.7 |

**Agent readiness 35.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 20.6** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/maven-machines/](https://apis.io/providers/maven-machines/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Maven Machines: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/maven-machines/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
