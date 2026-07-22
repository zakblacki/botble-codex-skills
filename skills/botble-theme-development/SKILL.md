---
name: botble-theme-development
description: Build, refactor, or review Botble CMS themes, child themes, layouts, partials, shortcodes, widgets, theme options, frontend routes, assets, RvMedia images, Theme facade usage, TailwindCSS v4 theme code, and view organization.
---

# Botble Theme Development

Use this for theme-side work under `platform/themes/{theme}`. Theme code has different translation and rendering rules from plugins.

## Workflow

1. Inspect the active theme structure and existing partials before adding files.
2. Keep Blade views focused; split files near 150 lines into partials.
3. Register assets and theme behavior from `config.php`, commonly inside `beforeRenderTheme`.
4. Use `Theme::scope()`, `Theme::partial()`, `theme_option()`, and Theme getters instead of ad hoc global access.
5. Create shortcodes with frontend views and admin config forms when content editors need controls.
6. Create widgets with separate frontend and backend templates.
7. Avoid DB queries in header/footer; use view composers or prepared data.

## Structure

```text
platform/themes/{theme}/
  assets/
  config.php
  functions/
  lang/
  layouts/
  partials/
  public/
  views/
  widgets/
  theme.json
  vite.build.mjs
```

## Rules

- Use `__('Text')` in themes and flat JSON language files.
- Use `trans()` only for plugin/package/core namespaces from theme code.
- Use `RvMedia::getImageUrl()` for all media paths.
- Use `Theme::getSiteTitle()`, `Theme::getLogo()`, and `Theme::getSiteCopyright()` where applicable.
- Use `ThemeSupport::registerSocialLinks()`, `registerPreloader()`, and related helpers instead of custom duplicated options.
- Register frontend routes through `Theme::registerRoutes()` when theme routes are needed.
- For multiple shortcode instances, generate unique slider/carousel IDs.
- Do not add CDN assets or inline scripts/styles.
- Declare theme asset entries in `vite.build.mjs`; do not add `webpack.mix.js`.

## Shortcodes

Use admin config fields such as `text`, `textarea`, `image`, `select`, `onOff`, `number`, `color`, and `tabs`. Sanitize HTML output and pass editor-controlled images through RvMedia.

## TailwindCSS v4 Themes

When the theme uses TailwindCSS v4:

- Keep configuration in CSS, not `tailwind.config.js`.
- Use `@source`, `@custom-variant dark`, and `@theme`.
- Use OKLCH colors when defining design tokens.
- Implement dark mode via the `.dark` class on `<html>`.

## Asset Builds

- Run `npm run dev` for an unminified build.
- Run `npm run production` for minified assets and the module-local `public/` mirror.
- Do not prescribe `npm run watch`; Botble's Vite pipeline has no watch mode or dev server.

## Load References

Read `references/theme-patterns.md` for compact snippets.
