# Theme Patterns

## Render a Scoped View

```php
return Theme::scope('shortcodes.hero', compact('shortcode'))->render();
```

## Render a Partial

```php
{!! Theme::partial('header') !!}
```

## Media URL

```blade
<img src="{{ RvMedia::getImageUrl($image, 'thumb') }}" alt="{{ $title }}">
```

## Theme Option

```php
$phone = theme_option('hotline');
```

## Shortcode Image Handling

```blade
@if ($image = $shortcode->image)
    <img src="{{ RvMedia::getImageUrl($image) }}" alt="{{ $shortcode->title }}">
@endif
```

## Child Theme

Use `inherit` in `theme.json` to declare the parent theme. Override only the needed layouts, partials, views, assets, or language entries.

## Vite Descriptor

```js
export default {
    js: [{ src: 'assets/js/theme.js', out: 'theme.js' }],
    sass: [{ src: 'assets/sass/style.scss', out: 'style.css' }],
}
```

Build from the project root with `npm run dev` or `npm run production`.

## View Composer Guidance

Prepare shared header/footer data in a composer or service provider. Do not run product, menu, or settings queries directly from repeated partials.
