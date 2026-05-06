---
name: botble-testing
description: Write, refactor, or review Botble CMS PHPUnit tests for plugins, themes, APIs, ecommerce features, permissions, requests, migrations, and regressions using RefreshDatabase, authenticated requests, real database assertions, and pre-commit verification commands.
---

# Botble Testing

Use focused tests that exercise Botble behavior through real framework code.

## Rules

- Use `RefreshDatabase` unless the local suite uses another database reset pattern.
- Test success and failure scenarios.
- Test permission-restricted admin routes.
- Use `$this->loginAs()` for authenticated admin test requests when available.
- Do not mock the database for model, repository, table, or controller behavior.
- Use factories only when they follow Botble model conventions and casts.
- Assert database state with real table names and meaningful columns.

## Coverage Targets

- Form requests validate required fields, enum values, and ownership.
- Controllers create, update, delete, and redirect with expected success/errors.
- API endpoints return the expected response envelope and resource payload.
- Ecommerce tests cover cart ownership, payment status transitions, and order state changes.
- Plugin lifecycle tests verify migrations/settings cleanup when lifecycle behavior is custom.

## Verification

Run the smallest useful command set:

- `php -l path/to/file.php`
- `./vendor/bin/pint`
- `php artisan test --filter=Name`
- `vendor/bin/phpunit --filter Name`

## Load References

Read `references/testing-patterns.md` for example tests.
