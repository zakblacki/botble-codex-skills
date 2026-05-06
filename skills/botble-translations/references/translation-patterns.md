# Translation Patterns

## Plugin PHP File

```php
return [
    'name' => 'Reviews',
    'create' => 'Create review',
    'edit' => 'Edit review ":name"',
    'customer_not_found' => 'L\'utilisateur n\'existe pas.',
];
```

Usage:

```php
trans('plugins/reviews::reviews.create');
```

## Theme JSON File

```json
{
  "Home": "Home",
  "Add to cart": "Add to cart",
  "Product :name is unavailable": "Product :name is unavailable"
}
```

Usage:

```php
__('Add to cart');
```

## Review Checklist

- No missing placeholders.
- No nested theme JSON arrays.
- No accidental array conversion for existing string keys.
- No unescaped apostrophes in single-quoted PHP strings.
