---
name: Token-gate access with Bitski
description: Create a token gate and check whether a wallet holds the required token.
api: openapi/bitski-nft-service-openapi-original.json
operations: [list, get, update, check]
---

# Token-gate access with Bitski

Limit access to pages or experiences to holders of a specific token using the
Bitski NFT Service gating APIs (base URL `https://api.bitski.com`).

## Auth
Backend-only application credentials (OAuth2 client credentials or HTTP Basic).
See `authentication/bitski-authentication.yml`.

## Steps
1. **Create a gate** — `POST /v1/apps/{app_id}/gates` (operationId `create`) defining the
   token/contract that grants access.
2. **List / read gates** — `GET /v1/apps/{app_id}/gates` (`list`) and
   `GET /v1/apps/{app_id}/gates/{gate_id}` (`get`); update with
   `PUT /v1/apps/{app_id}/gates/{gate_id}` (`update`).
3. **Check access at request time** — `GET /v1/gates/check` (`check`) to verify a
   wallet controls the required token before serving gated content.

## Notes
- Several gating operationIds (`create`, `list`, `get`, `update`) are generic in the
  source spec — disambiguate by method + path as shown above.
- Errors use the custom envelope (`errors/bitski-problem-types.yml`).
