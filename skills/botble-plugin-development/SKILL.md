---
name: botble-plugin-development
description: Scaffold, implement, refactor, or review Botble CMS plugins, including plugin.json, service providers, admin CRUD, models, migrations, repositories, forms, tables, routes, permissions, hooks, lifecycle methods, assets, translations, and Botble artisan generators.
---

# Botble Plugin Development

Use Botble conventions first, then apply this plugin-specific workflow.

## Workflow

1. Inspect nearby plugins before adding new structure.
2. Prefer Botble generators where available: `php artisan cms:plugin:create`, `cms:make:model`, `cms:make:form`, `cms:make:table`, `cms:make:controller`, `cms:make:request`, `cms:make:route`.
3. Create the plugin under `platform/plugins/{plugin}` with predictable namespaces, translations, routes, providers, migrations, and `plugin.json`.
4. Register admin routes through `AdminHelper::registerRoutes()` and use `wherePrimaryKey()` for route IDs.
5. Register permissions in `config/permissions.php` and attach them to dashboard menu items and routes.
6. Implement `activate()`, `deactivate()`, and `remove()` only when lifecycle work is needed. `remove()` must drop all plugin tables and clean plugin settings.
7. Run syntax, formatting, and targeted tests.

## Required Structure

```text
platform/plugins/your-plugin/
  config/general.php
  config/permissions.php
  database/migrations/
  resources/lang/en/your-plugin.php
  resources/views/
  routes/web.php
  routes/api.php
  src/Enums/
  src/Forms/
  src/Http/Controllers/
  src/Http/Requests/
  src/Models/
  src/Providers/
  src/Repositories/
  src/Services/
  src/Tables/
  src/Plugin.php
  plugin.json
```

## Implementation Rules

- Models extend `Botble\Base\Models\BaseModel`.
- Use `casts(): array`, not a `$casts` property, unless local code clearly still uses the property.
- Migrations use `foreignId()` and include proper cascade/null behavior.
- Controllers use Botble response helpers such as `withCreatedSuccessMessage()` and `withUpdatedSuccessMessage()`.
- Forms extend `FormAbstract` and use typed field classes with FieldOptions.
- Tables use typed column classes; use `FormattedColumn` for custom display.
- Use `trans('plugins/{plugin}::file.key')`, never `__()` in plugin code.
- Register SlugHelper, SeoHelper, LanguageAdvancedManager, DashboardMenu, hooks, and assets only when the plugin needs them.
- Use `BaseHelper::clean()` for unescaped HTML and `RvMedia::getImageUrl()` for media.

## Load References

- Read `references/examples.md` for model, form, table, provider, and route examples.
- Read `../botble-conventions/references/quick-reference.md` for baseline Botble rules.
