# Ecommerce Patterns

## Product List Query

```php
$products = Product::query()
    ->with(['slugable', 'categories', 'productLabels'])
    ->wherePublished()
    ->paginate(12);
```

Add any relation used by the target view or resource.

## Status Output

```php
'order_status' => [
    'value' => $order->status->getValue(),
    'label' => $order->status->label(),
],
```

## Price

```php
FormattedColumn::make('price')
    ->formatted(fn ($value) => format_price($value));
```

## Payment Gateway Review

Check that gateway code has settings, routes, webhook validation, payment service logic, and status mapping. Do not mark orders paid before webhook or gateway confirmation.
