---
name: Mint an NFT with Bitski
description: Create a contract, define a token template, and mint a token using the Bitski NFT Service APIs.
api: openapi/bitski-nft-service-openapi-original.json
operations: [create_contract, create_token_template, create_token, get_token]
---

# Mint an NFT with Bitski

Use the Bitski NFT Service APIs (base URL `https://api.bitski.com`) to deploy a
collection and mint tokens on an EVM chain.

## Auth
Call from your backend. Authenticate with your application credentials
(`CREDENTIAL_ID` / `CREDENTIAL_SECRET` from https://developer.bitski.com) using
OAuth2 client credentials (token endpoint `https://account.bitski.com/oauth2/token`)
or HTTP Basic `Authorization: Basic base64(CREDENTIAL_ID:CREDENTIAL_SECRET)`.
Never expose credentials in the browser.

## Steps
1. **Create a contract** — `POST /v1/apps/{app_id}/contracts` (`create_contract`) to
   deploy a dedicated or shared collection on your target chain.
2. **Create a token template** — `POST /v1/apps/{app_id}/token-templates`
   (`create_token_template`) describing the token metadata to mint from.
3. **Mint a token** — `POST /v1/apps/{app_id}/tokens` (`create_token`) referencing the
   contract and template.
4. **Confirm** — `GET /v1/apps/{app_id}/tokens/{token_id}` (`get_token`) to read back
   token details.

## Conventions
- Errors return a custom JSON envelope: `{ "error": { "code, status, request, message" } }`
  — capture `error.request` (UUID) for support. See `errors/bitski-problem-types.yml`.
- List endpoints use offset pagination (`limit`, `offset`). See `conventions/bitski-conventions.yml`.
- No idempotency key is documented — guard retries on write operations yourself.
