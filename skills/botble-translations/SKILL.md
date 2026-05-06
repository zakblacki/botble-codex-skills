---
name: botble-translations
description: Add, refactor, or review Botble CMS translations, plugin PHP language files, theme JSON language files, placeholders, apostrophe escaping, multilingual seed data, supported locales, and translatable strings across plugins, packages, core, and themes.
---

# Botble Translations

Translation rules differ by Botble layer. Choose the helper and file format from the target code location.

## Plugins, Packages, Core

- Use `trans('plugins/name::file.key')`, `trans('packages/name::file.key')`, or core namespaces.
- Do not use `__()` for plugin strings; it will not resolve namespaced keys.
- Store plugin strings in `resources/lang/{locale}/{file}.php`.
- Keep keys stable and grouped by file purpose.
- Do not convert a string key into an array if existing code expects a string.

## Themes

- Use `__('Text')` in Blade and PHP theme code.
- Store theme translations as flat key-value JSON files.
- Do not use nested arrays in theme JSON translation files.

## Content Rules

- Preserve placeholders exactly: `:name`, `:count`, `:attribute`.
- Escape apostrophes in single-quoted PHP strings: `L\'utilisateur`.
- Keep punctuation and capitalization natural per locale.
- Translate user-facing strings; leave class names, route names, config keys, and placeholders untouched.

## Supported Locales

Use these locale codes when broad coverage is requested:

`ar`, `bg`, `bn`, `cs`, `da`, `de`, `el`, `es`, `fa`, `fi`, `fr`, `he`, `hi`, `hu`, `id`, `it`, `ja`, `ko`, `lt`, `lv`, `ms`, `nb`, `nl`, `pl`, `pt`, `pt-BR`, `ro`, `ru`, `sk`, `sl`, `sr`, `sv`, `th`, `tr`, `uk`, `vi`, `zh`, `zh-TW`.

## Load References

Read `references/translation-patterns.md` for examples.
