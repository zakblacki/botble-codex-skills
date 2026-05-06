---
name: botble-ecommerce
description: Build, refactor, or review Botble CMS ecommerce features, product data, product variations, orders, carts, checkouts, payment gateways, ecommerce helpers, hooks, statuses, infinite product grids, API payloads, and performance-sensitive product queries.
---

# Botble Ecommerce

Use this when touching Botble ecommerce models, checkout, payment, orders, product queries, carts, or storefront product UI.

## Domain Model

- Product hierarchy: `Product` -> `ProductVariation` -> `ProductVariationItem`.
- Order lifecycle: `PENDING` -> `PROCESSING` -> `COMPLETED` or `CANCELED`.
- Key enums include `OrderStatusEnum`, `PaymentStatusEnum`, `ShippingStatusEnum`, `ProductTypeEnum`, and `StockStatusEnum`.
- Use Botble enum access rules: `getValue()`, `label()`, string cast, or constants as appropriate.

## Product Queries

- Use `Product::query()`.
- Eager load relations used by views/resources.
- When selecting image fields, include both `image` and `images` if accessors or galleries need them.
- Keep filters composable and preserve existing `EcommerceHelper` behavior.

## Payment Gateway Pattern

Follow the six-step pattern:

1. Define constants and gateway identifiers.
2. Register hook filters.
3. Implement the payment service.
4. Handle webhooks and status updates.
5. Register routes.
6. Add settings form fields.

## Hooks

Use ecommerce hooks instead of editing core checkout/order flow directly. Common categories include order status changes, checkout payment filters, product display filters, cart updates, and post-payment callbacks.

## Storefront

- Use Botble media helpers for product images.
- Use the existing infinite scroll pattern such as `bb-infinite-products-grid` when extending product grids.
- Keep price rendering through existing helpers such as `format_price()`.
- Preserve currency and language handling from ecommerce helpers.

## Load References

Read `references/ecommerce-patterns.md` for snippets.
