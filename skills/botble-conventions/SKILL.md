---
name: botble-conventions
description: Core Botble CMS coding conventions, architecture rules, security practices, translations, enum handling, media URLs, frontend constraints, and review guardrails. Use whenever editing Botble CMS projects, especially files under platform/, packages, plugins, themes, resources/views, routes, database migrations, seeders, or tests.
---

# Botble Conventions

Use this as the always-on baseline for Botble CMS work. Prefer existing project patterns and official Botble helpers over generic Laravel code.

## Load References

Read `references/quick-reference.md` when implementing or reviewing Botble code. Read task-specific skills for plugin, theme, API, ecommerce, seeder, translation, testing, or review work.

## Architecture

- Treat `platform/core`, `platform/packages`, `platform/plugins`, and `platform/themes` as modular boundaries.
- Use Botble artisan generators when available: `php artisan cms:make:model`, `cms:make:form`, `cms:make:table`, `cms:make:controller`, `cms:make:request`, `cms:make:route`.
- Dump Composer autoload after adding or moving platform modules.
- Use the root `vite-build.mjs` runner without editing it. Declare plugin, package, or theme assets in the module's `vite.build.mjs` descriptor.
- Delete legacy `webpack.mix.js` files after migrating their entries to Vite.
- Set `vue: true` when a Vite entry imports Vue SFCs. Do not bundle another Vue runtime; Botble externalizes it to `window.Vue`.

## Critical Rules

- Extend `Botble\Base\Models\BaseModel`, never plain Eloquent `Model`.
- Use `Model::query()` instead of the `DB` facade for model data.
- Eager load relations with `->with([...])` before rendering lists, cards, or API payloads.
- Prefer implicit route model binding. Type raw ID parameters as `int|string`, use `wherePrimaryKey()` for custom ID constraints, and use `$model->getKey()` when ID type matters.
- Define casts with a `casts(): array` method in Laravel 12+ style unless the project already uses a different local convention.
- Use `foreignId()` for foreign key columns in migrations.

## Botble Enums

Botble uses `Botble\Base\Supports\Enum`, not PHP native enums. The enum `$value` property is protected.

Correct:

- `$model->status->getValue()`
- `(string) $model->status`
- `$model->status->label()`
- `BaseStatusEnum::PUBLISHED()`
- `$model->status->getValue() === BaseStatusEnum::PUBLISHED`

Wrong:

- `$model->status->value`
- `$model->status === BaseStatusEnum::PUBLISHED`

Raw request values and query bindings do not need enum object conversion.

## Translations

- Plugins/packages/core: use `trans('plugins/name::file.key')`, not `__()`.
- Themes: use `__('Text')` with flat JSON language files.
- Never convert a string translation key to an array value.
- Preserve `:placeholders` exactly.
- Escape apostrophes in single-quoted PHP translations, for example `l\'exemple`.

## Security

- Use `{{ $value }}` for escaped output.
- Use `BaseHelper::clean($html)` before any `{!! !!}` output.
- Use `@json($data)` when embedding data into JavaScript.
- Send `X-CSRF-TOKEN` for AJAX requests that mutate state.
- Read cookies through `request()->cookie()` and validate names/values against an allowlist.
- Do not add CDN assets; bundle libraries locally or use Botble helpers such as `BaseHelper::googleFonts()`.
- Keep dependencies current and check `npm outdated` when changing frontend dependencies.

## Media

- Always render media paths through `RvMedia::getImageUrl($path)`.
- Use presets with `RvMedia::getImageUrl($path, 'thumb')`.
- Never use raw `<img src="{{ $model->image }}">`.

## Frontend

- Use jQuery `.on()` event handlers, not `.click()`, `.bind()`, or `.hover()`.
- Do not add inline JavaScript or CSS attributes.
- Delete unused code instead of commenting it out.
- Pair Tabler badge classes, for example `bg-green text-green-fg`.

## Quality Gate

Before handing work back, run the narrowest useful checks:

- PHP syntax for changed PHP files: `php -l path/to/file.php`.
- Formatting: `./vendor/bin/pint` or the project equivalent.
- Tests: `vendor/bin/phpunit`, `php artisan test`, or targeted tests.
- Assets: `npm run dev` for development or `npm run production` for a production build. Botble's Vite pipeline has no watch mode or dev server.
