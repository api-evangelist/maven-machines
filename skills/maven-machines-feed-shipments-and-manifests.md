---
name: maven-machines-feed-shipments-and-manifests
description: >-
  Keep Maven's dispatch board in step with a TMS by continuously upserting shipments and pickup
  requests, assigning them to P&D manifests, and cancelling cleanly when the load falls through.
api: Maven Integrations API
base_url: https://integrations.mavenmachines.com
generated: '2026-08-25'
method: generated
source: >-
  openapi/maven-machines-planning-and-dispatch-openapi.json,
  openapi/maven-machines-shipments-openapi.json,
  openapi/maven-machines-shipment-locations-openapi.json,
  openapi/maven-machines-rest-service-manual-openapi.json,
  https://maven-machines.readme.io/docs/standard-tms-integration
operations:
- post-shipment
- shipmentbulkupsert
- post-companiescompanyidcustomers
- post-pickuprequestscancel
- ShipmentController_updateShipmentProNumber
- ShipmentLocationsController_upsertShipmentLocations
- post-manifests
- post-manifestnumber
- patch-manifestsmanifestnumber
---

# Feed shipments and P&D manifests from a TMS

The shipment feed is the one integration nearly every Maven fleet needs. Everything else is optional.

## Rule of thumb

**Anytime the shipment changes in the TMS, call Maven.** `POST /shipment` is designed to take
continuous updates — new EDI pickup requests, reweighs, billing updates, delivery-date adjustments.
It is an upsert keyed on your identifiers, so re-sending the same payload converges rather than
duplicating.

## Steps

1. **Customers** — `POST /customers` (`post-companiescompanyidcustomers`) adds or updates the
   billing/consignee party.
2. **Shipments** — `POST /shipment` (`post-shipment`) per change. For backfills and catch-up after
   an outage use `POST /shipment/bulkUpsert` (`shipmentbulkupsert`) instead of a tight loop.
3. **PRO numbers** — when the TMS assigns or re-assigns a PRO, call
   `POST /shipment/updateShipmentProNumber` (`ShipmentController_updateShipmentProNumber`) with the
   current and new PRO.
4. **Locations** — `POST /shipment-locations`
   (`ShipmentLocationsController_upsertShipmentLocations`) sets a shipment's current and/or moveTo
   location.
5. **Manifests** — `POST /manifests` (`post-manifests`) creates or updates the manifest that shows
   on the dispatch board. When Maven's planner generates the manifest and your TMS is the record
   keeper, assign your number with `POST /manifestNumber` (`post-manifestnumber`). Partial updates
   go through `PATCH /manifests/{manifestNumber}` (`patch-manifestsmanifestnumber`) — only the keys
   you send are changed.

## Undoing

If a pickup falls through, call `POST /pickupRequests/cancel` (`post-pickuprequestscancel`). Maven
publishes **no time window** for this — do not assume one. There is no reversal for a shipment
upsert itself; correct it by sending the corrected state.

## Reconciling

Do not poll the shipment endpoints for state. Read Maven's side of the conversation from
`GET /return-events` — see the `maven-machines-consume-return-events` skill.
