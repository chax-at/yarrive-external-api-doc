# Yarrive API

An API for external systems to connect to Yarrive, offering support for reading and synchronizing various sets of data.
Synchronization happens per Institution.

## Browse docs in browser
Install 
`npm ci`

Run Server
`npm start`

Browse [http://localhost:8080](http://localhost:8080).

## How to get an API-Key?
1. **In Yarrive**, as **Operator**, request an API-Key for your Yarrive-Institution. (`Administration` --> `API`)
    * This API-Key can then be used to access the API documented in `yarrive.api.json`.\
    * The API-Key should be stored **per Institution** in your external system and serves to identify and authenticate the linked Institution.\
    * The API-Key must be passed with each request as the header field `X-Api-Key`.

## Synchronization
1. Make sure your external system implements the API defined in `external-service.api.json`.
1. To **initiate Synchronization**, use the API-Key in the external system to call the `POST /sync` endpoint with the body `{ apiKey: '<your api key>' }`.\

### Initiate Synchronization per Entity
Individual Entities existing on Yarrive are by default **unsynched**. The following events will make them **synched**.
* Every **new** Entity related to the Institution created on Yarrive will be sent to the external System via a `POST` request.
* For **existing** (but yet unsynched) Entities, the external system has to perform a **read** operation (`GET`) first to prime them for synchronization.
* Entities **existing on the external system** have to be sent to Yarrive with the corresponding `POST` request.


Each synched Entity will feature a `syncId` which should be mirrored on the external system.
As soon as a `syncId` is present, a (supported) Entity will submit updates and deletions to the external system and also expects updates back.

## Example

TODO