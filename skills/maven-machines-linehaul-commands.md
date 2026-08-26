---
name: maven-machines-linehaul-commands
description: >-
  Drive Maven's event-sourced linehaul network correctly — send commands rather than CRUD, carry
  stable referenceIds, never blind-retry, and reverse with the paired compensating command instead
  of trying to erase history.
api: Maven Integrations API
base_url: https://integrations.mavenmachines.com
generated: '2026-08-25'
method: generated
source: >-
  https://maven-machines.readme.io/docs/commands-and-event-sourcing,
  https://maven-machines.readme.io/docs/command-reference,
  https://maven-machines.readme.io/docs/manifests-and-movements,
  openapi/maven-machines-manifest-commands-openapi.json,
  openapi/maven-machines-linehaul-openapi.json
operations:
- ManifestCommandsController_applyManifestCommands
- LinehaulController_upsertLinehaulManifest
- LinehaulController_upsertLinehaulTrip
---

# Drive Maven linehaul with commands

Maven's linehaul system is **event sourced**. You do not update a manifest; you tell Maven what
happened and Maven appends the event.

## The endpoint

`POST /manifests/commands` — `ManifestCommandsController_applyManifestCommands`. One endpoint for
manifest *and* movement commands, because movements belong to manifests. It accepts an array, so
batch when volume is high and send one at a time when it is not.

## Command shape

```json
{
  "commandType": "ArriveMovement",
  "payload":     { },
  "referenceIds": { },
  "eventSource": { "userId": "12093", "displayName": "Kent, Clark", "system": "AS400" }
}
```

- `commandType` — the intent, present tense (`CreateManifest`, `ArriveMovement`).
- `referenceIds` — **your** identifiers (e.g. a loadId). They must be unique and **constant for the
  whole lifecycle of the object**. Every later command for that manifest carries the same
  referenceIds. Get this wrong and you cannot address the object again.
- `eventSource` — who did it. `displayName` may be `"SYSTEM"` when there is no user. This is the
  audit trail; fill it in.

Validation runs first. A command that fails validation is rejected; a command that passes produces a
past-tense event (`ArriveMovement` → `MovementArrived`) that can never be updated or deleted.

## Do not blind-retry

This endpoint is **not idempotent**. There is no `Idempotency-Key` and no dedupe key. A retry after
a timeout can append a second event. On an ambiguous failure, reconcile from `GET /return-events`
before resending.

## Reversing

There is no undo. Reverse with the paired compensating command:

| Did | Undo with |
|---|---|
| `CreateManifest` | `CancelManifest` |
| `PlanShipmentsOnManifest` | `RemoveShipmentsFromManifest` |
| `LoadShipmentsOnManifest` | `UnloadShipmentsOnManifest` |
| added a movement | `DeleteMovement` |

`CancelManifest` cancels the manifest and all its movements and removes it from the Maven UI. It is
itself reversible — a cancelled manifest can be updated by other commands and becomes visible
again — but **new movements cannot be added to a cancelled manifest**. Maven states no time window
for any of these; do not assume one.

## The non-command path

Bulk state, rather than actions, goes through the two upserts:
`POST /linehaul/manifest` (`LinehaulController_upsertLinehaulManifest`) and
`POST /linehaul/trip` (`LinehaulController_upsertLinehaulTrip`). Those are safe to re-send.
