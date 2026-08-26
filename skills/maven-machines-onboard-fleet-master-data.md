---
name: maven-machines-onboard-fleet-master-data
description: >-
  Seed a Maven Machines fleet with the master data the platform needs before any freight can be
  dispatched — drivers/admins, power units, trailers, and the company locations where freight is
  picked up and delivered — using the caller's own external identifiers so every call is re-runnable.
api: Maven Integrations API
base_url: https://integrations.mavenmachines.com
generated: '2026-08-25'
method: generated
source: >-
  openapi/maven-machines-users-openapi.json, openapi/maven-machines-assets-openapi.json,
  openapi/maven-machines-company-locations-openapi.json,
  https://maven-machines.readme.io/docs/standard-tms-integration
operations:
- UsersController_createUser
- UsersController_updateUser
- UsersController_getUsers
- CreateVehicleController_createVehicle
- UpdateVehicleController_updateVehicle
- GetAllVehiclesController_getVehicles
- UploadVehiclesController_upload
- CreateTrailerController_createTrailer
- UpdateTrailerController_updateTrailer
- UploadTrailerController_upload
- CompanyLocationsController_createCompanyLocation
- CompanyLocationsController_patchCompanyLocation
- CompanyLocationsController_handleGetCompanyLocations
---

# Onboard a fleet's master data into Maven

Master data must exist before Maven will accept transactional freight. Do it in this order.

## Before you start

- Send the `apiKey` header on **every** call. The key identifies the fleet AND the environment;
  a staging key will not work against production.
- Develop against staging (`https://integrations-staging.mavenmachines.com`). Staging and
  production share no data.
- Decide your external identifiers now. Maven stores an `externalUserId`,
  `externalCompanyLocationId`, `vehicleNumber` and `trailerNumber` supplied by you, and matching on
  them is what makes these calls safe to re-run. Where you send both a Maven id and an external id,
  **Maven resolves on the Maven id first**.

## 1. Users (drivers and admins)

- `POST /users` — `UsersController_createUser`. Create from your HR system or TMS; Maven does not
  require you to manage users in its admin portal.
- `PUT /users` — `UsersController_updateUser`. Supply `userId` **or** `externalUserId`.
- `GET /users` — `UsersController_getUsers` to reconcile.

## 2. Power units and trailers

- `POST /vehicles` — `CreateVehicleController_createVehicle`. **Create-only**: if the
  `vehicleNumber` already exists the request is rejected. On a retry after an ambiguous failure,
  `GET /vehicles/{vehicleNumber}` (`GetVehiclesController_getVehicles`) first, then
  `PATCH /vehicles/{vehicleNumber}` (`UpdateVehicleController_updateVehicle`) — do not blind-retry
  the POST.
- `POST /trailers` — `CreateTrailerController_createTrailer`, same rule.
- Bulk seeding: `POST /vehicles/upload` (`UploadVehiclesController_upload`) and
  `POST /trailers/upload` (`UploadTrailerController_upload`) take a CSV with a fixed column set and
  a `ChgType` of 1 (add), 2 (deactivate) or 3 (update). **Maximum 1000 rows per file** — chunk
  larger fleets.

## 3. Company locations

- `POST /company-locations` — `CompanyLocationsController_createCompanyLocation`. This models
  terminals, warehouses, depots and, most often, the customers where freight moves.
- `PATCH /company-locations` — `CompanyLocationsController_patchCompanyLocation` on every customer
  update in the TMS. Supply `companyLocationId` or `externalCompanyLocationId`.
- `GET /company-locations` — `CompanyLocationsController_handleGetCompanyLocations`; paginate with
  `offset`.

## Errors

Maven returns `{ "type": ..., "message": ... }`. `BAD_REQUEST` (400) means fix the payload and
retry; `UNAUTHORIZED` (401) means the `apiKey` is missing or not authorized for this fleet;
`SERVER_ERROR` (500) is safe to retry with backoff on the upsert-shaped calls only. See
`errors/maven-machines-problem-types.yml`.
