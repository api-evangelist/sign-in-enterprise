---
name: Maintain watchlists for visitor screening
description: Create and maintain watchlists so incoming visitors and sign-ins are screened against denied parties.
api: openapi/sign-in-enterprise-guest-api-openapi-original.yml
operations: [getWatchlists, createWatchlist, getWatchlist, updateWatchlist, deleteWatchlist]
---

# Maintain watchlists for visitor screening

Manage the watchlists that Sign In Enterprise screens visitors against.

## Auth
- OAuth 2.0 / OpenID Connect bearer token. Request scopes `watchlists:read`, `watchlists:write`.
- Base URL: `https://us.tractionguest.com/api/v3`.

## Steps
1. **List watchlists.** Call `getWatchlists` (GET /watchlists) to see existing lists.
2. **Create a watchlist.** Call `createWatchlist` (POST /watchlists). Send an `Idempotency-Key` header for safe retries.
3. **Inspect one.** Call `getWatchlist` (GET /watchlists/{watchlist_id}).
4. **Update entries.** Call `updateWatchlist` (PUT /watchlists/{watchlist_id}) to add or amend denied parties.
5. **Remove a list.** Call `deleteWatchlist` (DELETE /watchlists/{watchlist_id}) when it is no longer needed.

## Conventions
- Idempotency: `Idempotency-Key` header on writes.
- Pagination: `limit` / `offset`.
- Errors: 400/401/403/404/422 JSON — see errors/sign-in-enterprise-problem-types.yml.
