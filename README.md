# Yarrive API

An API for external systems to connect to Yarrive, offering support for reading and synchronizing various sets of data.
Synchronization happens per Institution.

> ## Browse here:
> https://chax-at.github.io/yarrive-external-api-doc


### ...or build and browse locally:
Clone and install:
```
git clone https://github.com/chax-at/yarrive-external-api-doc.git
cd yarrive-external-api-doc
npm ci
```

Serve:
```
npm start
```

Docs can then be reached at [http://localhost:8080](http://localhost:8080).

## How to get an API-Key?
1. **In Yarrive**, as **Operator**, request an API-Key for your Yarrive-Institution. (`Administration` --> `API`)
    * This API-Key can then be used to access the API documented in `yarrive.api.json`.\
    * The API-Key should be stored **per Institution** in your external system and serves to identify and authenticate the linked Institution.\
    * The API-Key must be passed with each request as the header field `X-Api-Key`.

## Synchronization
1. Make sure your external system implements the API defined in `external-service.api.json`.
1. To **initiate Synchronization**, use the API-Key in the external system to call the `POST /sync` endpoint with the body `{ apiKey: '<your api key>' }`.\

### Initiate Synchronization per Entity
Individual Entities existing on Yarrive are by default **unsynced**. The following events will make them **synced**.
* Every **new** Entity related to the Institution created on Yarrive will be sent to the external System via a `POST` request.
* For **existing** (but yet unsynced) Entities, the external system has to perform a **read** operation (`GET`) first to prime them for synchronization.
* Entities **existing on the external system** have to be sent to Yarrive with the corresponding `POST` request.


Each synced Entity will feature a `syncId` which should be mirrored on the external system.
As soon as a `syncId` is present, a (supported) Entity will submit updates and deletions to the external system and also expects updates back.

## Example

TODO