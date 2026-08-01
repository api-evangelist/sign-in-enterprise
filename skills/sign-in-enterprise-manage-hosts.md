---
name: Provision and manage hosts
description: Create hosts on the fly (single or in bulk) so employees can receive and approve visitors without CSV uploads.
api: openapi/sign-in-enterprise-guest-api-openapi-original.yml
operations: [getHosts, createHost, createHosts, getBatch]
---

# Provision and manage hosts

Keep the employee/host directory in sync so visitors can be matched to the right person.

## Auth
- OAuth 2.0 / OpenID Connect bearer token. Request scope `hosts:write` (and `hosts:read`).
- Base URL: `https://us.tractionguest.com/api/v3`.

## Steps
1. **List existing hosts.** Call `getHosts` (GET /hosts) to check who is already provisioned.
2. **Create one host.** Call `createHost` (POST /hosts) with the employee's name/email. Send an `Idempotency-Key` header for safe retries.
3. **Bulk-create hosts.** For onboarding many employees, call `createHosts` (POST /hosts/batch). This returns a batch job.
4. **Track the batch.** Poll `getBatch` (GET /batches/{batch_id}) until the bulk host creation completes.

## Conventions
- Idempotency: `Idempotency-Key` header on writes (24h, min 10 chars).
- Pagination: `limit` / `offset`.
- Errors: 400/401/403/404/422 JSON — see errors/sign-in-enterprise-problem-types.yml.
