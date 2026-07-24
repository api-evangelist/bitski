---
name: Sell NFTs with Bitski Commerce
description: List products, add a payment method, and purchase NFTs via credit card, ACH, or crypto.
api: openapi/bitski-nft-service-openapi-original.json
operations: [list_products, get_product, add_payment_method, create_order, patch_order_payment, get_order]
---

# Sell NFTs with Bitski Commerce

Drive an NFT storefront checkout with the Bitski NFT Service APIs
(base URL `https://api.bitski.com`). Buyers can pay by credit card, ACH, or crypto.

## Auth
Backend-only, using application credentials via OAuth2 client credentials or HTTP
Basic (see `authentication/bitski-authentication.yml`).

## Steps
1. **Browse the catalog** — `GET /v1/products` (`list_products`) and
   `GET /v1/products/{product_id}` (`get_product`) to show items from a storefront.
2. **Attach a payment method** — `POST /v1/users/{user_id}/payment-methods`
   (`add_payment_method`); list existing ones with `GET /v1/users/{user_id}/payment-methods`
   (`list_payment_methods`).
3. **Create the order** — `POST /v1/orders` (`create_order`) to purchase the NFT(s).
4. **Set/adjust payment** — `PATCH /v1/orders/{order_id}/payments/{payment_id}`
   (`patch_order_payment`) if the buyer changes payment method.
5. **Track the order** — `GET /v1/orders/{order_id}` (`get_order`).

## Conventions
- Custom error envelope with `error.request` UUID (`errors/bitski-problem-types.yml`).
- Offset pagination (`limit`/`offset`) on list calls.
- Activity Webhooks can notify you of on-chain results
  (`asyncapi/bitski-activity-webhooks.yml`, sales-gated).
