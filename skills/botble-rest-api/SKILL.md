---
name: botble-rest-api
description: Build, refactor, or review Botble CMS REST APIs for mobile apps or integrations, including BaseApiController responses, JSON resources, Sanctum authentication, optional guest auth, API headers, rate limiting, guest carts, routes/api.php, and API security.
---

# Botble REST API

Use Botble's API response and auth conventions instead of generic Laravel JSON controllers.

## Controller Pattern

- Extend `BaseApiController` when the project provides it.
- Return API responses through `$this->httpResponse()->setData(...)->toApiResponse()`.
- Keep the response shape consistent: `{"error": false, "data": ..., "message": null}`.
- Transform models with JSON Resources instead of returning raw models.
- Sanitize or cast user-controlled output before exposing rich HTML.

## Routes and Auth

- Put API routes in `routes/api.php`.
- Use `auth:sanctum` for authenticated customer/user endpoints.
- Use `api.optional.auth` for guest-capable features such as carts.
- Use named throttle limiters through `ThrottleRequests::using('name')` when available.
- Support custom headers used by Botble integrations: `X-API-KEY`, `X-CURRENCY`, `X-LANGUAGE`, and `X-API-IP`.

## Guest Features

- For carts and wishlist-like flows, support authenticated IDs and guest UUIDs.
- Prefer `$customerId ?? Str::uuid()` style assignment only after checking local cart ownership rules.
- Never let a guest token or UUID access another customer's data.

## Implementation Rules

- Use `Model::query()` and eager loading.
- Validate request payloads with Form Request classes.
- Type IDs as `int|string`.
- Avoid exposing internal enum objects; return enum value and label when useful.
- Preserve pagination metadata for list endpoints.

## Load References

Read `references/api-patterns.md` for snippets.
