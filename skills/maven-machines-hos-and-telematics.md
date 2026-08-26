---
name: maven-machines-hos-and-telematics
description: >-
  Read a Maven fleet's regulated hours-of-service state and live vehicle telematics — duty-status
  summaries, remaining-clock timers, ping history and latest-position snapshots — for planning and
  compliance monitoring.
api: Maven Integrations API
base_url: https://integrations.mavenmachines.com
generated: '2026-08-25'
method: generated
source: >-
  openapi/maven-machines-rest-service-manual-openapi.json,
  openapi/maven-machines-eld-hos-openapi.json,
  https://maven-machines.readme.io/docs/eld-return-events
operations:
- get-hoslogssummary
- get-hostimerssnapshot
- post-hosdutystatus
- get-locationsvehicles
- get-locationsvehiclessnapshot
---

# Read hours-of-service and telematics

## Hours of service

- `GET /eld/hos/logs/summary` (`get-hoslogssummary`) — "summarized ELD information for all active
  drivers in a given fleet". Duty-status durations use the regulated vocabulary:
  `ON_DUTY_NOT_DRIVING`, `DRIVING`, `SLEEPER_BERTH`.
- `GET /eld/hos/timers/snapshot` (`get-hostimerssnapshot`) — remaining-clock state. Use this, not
  the log summary, when deciding whether a driver can legally take a load.
- `POST /eld/hos/dutystatus` (`post-hosdutystatus`) — write a duty status.

Violations do not arrive here. They come through the return-events queue as `violationCreated` and
`violationInvalidated` — an invalidation means a previously raised violation was withdrawn, so
never treat `violationCreated` as final on its own.

## Telematics

- `GET /locations/vehicles` (`get-locationsvehicles`) — "a history of all recorded telematics pings
  for any vehicle that is installed with a Maven Vehicle Data Adapter (VDA)". History; paginate.
- `GET /locations/vehicles/snapshot` (`get-locationsvehiclessnapshot`) — latest ping per vehicle
  across the fleet. This is the one to poll for a live map.

Only vehicles fitted with a Maven VDA report. A vehicle present in `GET /vehicles` but absent from
the snapshot is un-instrumented, not offline — check before alerting.

## Caution

This is regulated data. Maven publishes no rate limits, so pace your own polling; the snapshot
endpoints are the cheap ones and the history endpoints are not.
