---
name: Fetch a verified identity and its resources
description: Retrieve an identity from the Passbase Verifications API and read the resources (documents, datapoints) attached to it.
api: openapi/passbase-verification-openapi.yml
operations: [listIdentities, getIdentityById, listIdentityResources, getIdentityResourceById]
---

# Fetch a verified identity and its resources

> Historical note: Passbase was acquired by Parallel Markets (2023) and
> `api.passbase.com` is no longer live. This skill documents the last-published
> Verifications API v2 behavior.

## Auth
Send the secret API key in the `X-API-KEY` request header. Server-to-server
calls require the secret key (never the publishable key). See
`authentication/passbase-authentication.yml`.

## Steps

1. **List identities** — call `listIdentities` (`GET /identities`). Page with the
   `limit` and `cursor` query params; the response `cursor.next` is an opaque
   token for the next batch (see `conventions/passbase-conventions.yml`).
2. **Get one identity** — call `getIdentityById` (`GET /identities/{id}`) with the
   identity `id`. Read `status`, `score` (0–1 confidence), `owner`, and any
   `metadata` you passed through the client SDK.
3. **List its resources** — call `listIdentityResources`
   (`GET /identity/{id}/resources`) to enumerate the source documents attached to
   the identity.
4. **Get one resource** — call `getIdentityResourceById`
   (`GET /identity/{id}/resources/{resource_id}`) to read a single resource and
   its extracted datapoints.

## Errors
Handle `401` (bad/missing key), `403` (insufficient authorization — the raw
resource-file route needs specific government authorization), `404` (unknown
identity/resource), and `429` (rate limited). See
`errors/passbase-problem-types.yml`.
