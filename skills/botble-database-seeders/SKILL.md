---
name: botble-database-seeders
description: Create, refactor, or review Botble CMS database seeders, demo content, theme seeders, translated seed data, media fixtures, realistic ecommerce products, content HTML files, and seeder assets while avoiding Faker for user-visible content.
---

# Botble Database Seeders

Generate demo data that looks deliberate and marketplace-ready.

## Core Rules

- Do not use `fake()` or Faker for user-visible names, titles, descriptions, slugs, addresses, or content.
- Use realistic product names, prices, categories, descriptions, and page content.
- Store reusable HTML content in `database/seeders/contents/`.
- Store demo images and files in `database/seeders/files/`.
- Support multilingual demo content through `database/seeders/translations/{locale}/`.
- Use `Arr::random()` for variety over curated arrays.

## Faker Is Acceptable For

- Passwords such as `bcrypt('12345678')`.
- Random selection from curated arrays.
- Random counts such as `rand(3, 8)`.
- Random booleans such as `rand(0, 1)` for `is_featured`.

## Structure

```text
database/seeders/
  DatabaseSeeder.php
  TranslationSeeder.php
  contents/
  files/
  translations/{locale}/
    ec_products.json
    {model}-content.html
  Themes/Main/
```

## Implementation

- Use model factories only if they produce curated, user-facing values.
- Use `Model::query()` for reads and updates.
- Use existing Botble helpers for slugs, media, settings, ecommerce data, and translations.
- Keep seeders idempotent where practical with truncate/recreate or update-or-create patterns used by the project.
- Do not reference placeholder image URLs.
- Use JSON translation files for translated seed content and preserve entity keys.

## Load References

Read `references/seeder-patterns.md` for structure and examples.
