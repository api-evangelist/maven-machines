---
name: maven-machines-consume-return-events
description: >-
  Run a correct polling loop against Maven's return-events queue — cursor handling, paging, the
  30-day retention cliff, and the two different event-naming conventions — so a downstream system
  stays in step with what drivers and dispatchers actually did.
api: Maven Integrations API
base_url: https://integrations.mavenmachines.com
generated: '2026-08-25'
method: generated
source: >-
  https://maven-machines.readme.io/docs/return-events,
  https://maven-machines.readme.io/docs/pagination,
  https://maven-machines.readme.io/docs/pd-return-events,
  https://maven-machines.readme.io/docs/linehaul-dock-app-return-events,
  https://maven-machines.readme.io/docs/eld-return-events,
  openapi/maven-machines-rest-service-manual-openapi.json
operations:
- get-return-events
- get-events
---

# Consume Maven return events

Maven does **not** push. There are no webhooks and no AsyncAPI document. Everything Maven has to
tell you arrives through a polled queue.

## The loop

- `GET /return-events` (`get-return-events`) with a `startTime` cursor, an ISO 8601 UTC string:
  `GET /return-events?startTime=2024-01-01T17:00:00.000Z`
- Poll on a fixed interval. Maven recommends **every 30 seconds to 1 minute**.
- Set the cursor to `now - interval` on each pass. Persist the cursor; do not hold it in memory
  only.
- A busy fleet or a long interval can produce more events than fit in one page — keep reading until
  the page is short before advancing the cursor.

## The retention cliff

Events live **30 days** and are then deleted permanently. There is no replay and no dead-letter. If
your consumer is down for a month, that data is gone — treat a stalled cursor as a page-worthy
incident, not a warning.

## Envelope

Every event is `{ id, timestamp, eventType, data }`. Branch on `eventType`.

## Two naming conventions — this will bite you

- P&D events are **camelCase**: `shipmentCreated`, `stopArrival`, `stopComplete`, `routeStart`,
  `routeETAUpdate`, `manifestDispatched`, `geofenceTerminalArrival`, `customerUpdated`, …
- Linehaul / Dock App events are **PascalCase**: `ManifestCreated`, `MovementArrived`,
  `MovementDeparted`, `MovementAssignedToDriver`, `MovementDeleted`, `FinishedUnloadingManifest`, …
- ELD events: `violationCreated`, `violationInvalidated`.

Match exactly. Do not normalize case in your router — `manifestCreated` and `ManifestCreated` are
different events from different products.

## Documents

Bills of lading, shipment photos and signatures are **not** in the event payload. Retrieve them
separately — see https://maven-machines.readme.io/docs/retrieving-documents-from-return-events.

The full catalog of event types this profile captured is in
`asyncapi/maven-machines-return-events.yml`.
