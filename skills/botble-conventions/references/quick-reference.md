# Botble Quick Reference

## Enum Values

```php
$model->status->getValue();
$model->status->label();
(string) $model->status;
BaseStatusEnum::PUBLISHED;
BaseStatusEnum::PUBLISHED();
$model->status->getValue() === BaseStatusEnum::PUBLISHED;
```

Avoid `$enum->value` and object-to-string `===` comparisons.

## Translations

```php
trans('plugins/blog::posts.create'); // plugins, packages, core
__('Home');                          // themes only
```

Use flat strings, preserve `:placeholders`, and escape apostrophes in single-quoted PHP arrays.

## Eloquent

```php
Post::query()
    ->with(['author', 'categories'])
    ->where('status', BaseStatusEnum::PUBLISHED)
    ->get();
```

Use `int|string` IDs and `$model->getKey()` when UUID support matters.

## Forms

```php
NameFieldOption::make()->required();
StatusFieldOption::make();
```

Use typed field classes and modern FieldOptions.

## Tables

```php
FormattedColumn::make('price')
    ->formatted(fn ($value) => format_price($value));
```

Use `FormattedColumn` for custom rendering callbacks.

## Security

```php
BaseHelper::clean($html);
@json($data);
request()->cookie('name');
```

Validate cookie names and values against an allowlist.

## Images

```php
RvMedia::getImageUrl($path);
RvMedia::getImageUrl($path, 'thumb');
```

Never render raw stored media paths.

## Routes and Responses

```php
Route::get('{id}', [Controller::class, 'edit'])->wherePrimaryKey();

return $this
    ->httpResponse()
    ->setPreviousUrl(route('plugin.index'))
    ->withCreatedSuccessMessage();
```

## Assets

```text
vite-build.mjs                       # shared root runner; do not edit
platform/plugins/name/vite.build.mjs # module descriptor
npm run dev                          # development build
npm run production                   # production build and module-public mirror
```

Do not add new `webpack.mix.js` files or document a Vite watch/dev-server workflow.
