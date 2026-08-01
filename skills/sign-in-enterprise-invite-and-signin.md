---
name: Invite a visitor and record their sign-in
description: Create a pre-registered invite for a location, then look up and update the visitor's sign-in when they arrive.
api: openapi/sign-in-enterprise-guest-api-openapi-original.yml
operations: [getLocations, createLocationInvite, getInvite, updateInvite, getSignins, getSignin, updateSignin]
---

# Invite a visitor and record their sign-in

Use the Sign In Solutions VMS API to pre-register a visitor and manage their arrival.

## Auth
- OAuth 2.0 / OpenID Connect bearer token. Request scopes `locations:read`, `visitors:write`.
- Base URL: `https://us.tractionguest.com/api/v3`.

## Steps
1. **Find the location.** Call `getLocations` (GET /locations) and select the `location_id` for the site the visitor will attend.
2. **Create the invite.** Call `createLocationInvite` (POST /locations/{location_id}/invites) with the visitor's details. For safe retries, send an `Idempotency-Key` header (stored 24h, min 10 chars).
3. **Confirm the invite.** Call `getInvite` (GET /invites/{invite_id}) to verify; use `updateInvite` (PUT /invites/{invite_id}) to amend details before arrival.
4. **On arrival, find the sign-in.** Call `getSignins` (GET /signins) filtered to the location/visitor, or `getSignin` (GET /signins/{signin_id}).
5. **Update the sign-in** if needed with `updateSignin` (PUT /signins/{signin_id}) — e.g. to sign the visitor out.

## Conventions
- Idempotency: `Idempotency-Key` header on writes.
- Pagination: `limit` / `offset` on list operations.
- Errors: 400/401/403/404/422 JSON — see errors/sign-in-enterprise-problem-types.yml.
