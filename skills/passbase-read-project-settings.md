---
name: Read project verification settings
description: Read the Passbase project settings, including customizations and the required verification steps.
api: openapi/passbase-verification-openapi.yml
operations: [getSettings]
---

# Read project verification settings

> Historical note: the live Passbase API is discontinued (acquired by Parallel
> Markets, 2023). This documents the last-published behavior.

## Auth
Send the secret API key in the `X-API-KEY` header. See
`authentication/passbase-authentication.yml`.

## Steps

1. **Get settings** — call `getSettings` (`GET /settings`). The `ProjectSettings`
   response includes:
   - `id`, `slug`, `environment`, `organization`
   - `customizations` (button color, accent color, font family)
   - `verification_steps` — the ordered steps a user must complete, each with its
     allowed `resource_types`.

Use `verification_steps` to understand what a user will be asked to submit before
you initiate a verification flow.

## Errors
Handle `401` for a missing/invalid API key. See
`errors/passbase-problem-types.yml`.
