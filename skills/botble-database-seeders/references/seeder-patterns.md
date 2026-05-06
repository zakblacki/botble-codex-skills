# Seeder Patterns

## Curated Data

```php
$products = [
    [
        'name' => 'Hydrating Rose Face Cream',
        'price' => 29.90,
        'description' => 'A lightweight daily moisturizer with rose extract and hyaluronic acid.',
    ],
    [
        'name' => 'Vitamin C Brightening Serum',
        'price' => 34.50,
        'description' => 'A concentrated serum for dull and uneven-looking skin.',
    ],
];
```

## Variety

```php
use Illuminate\Support\Arr;

$category = Arr::random($categories);
$isFeatured = rand(0, 1);
```

## Translations Layout

```text
database/seeders/translations/fr/ec_products.json
database/seeders/translations/fr/page-content.html
```

Preserve identifiers so translations can be mapped back to seeded records.
