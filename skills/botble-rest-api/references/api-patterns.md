# API Patterns

## Response

```php
return $this
    ->httpResponse()
    ->setData(ProductResource::make($product))
    ->toApiResponse();
```

## Collection

```php
$products = Product::query()
    ->with(['categories', 'slugable'])
    ->paginate((int) $request->integer('per_page', 12));

return $this
    ->httpResponse()
    ->setData(ProductResource::collection($products))
    ->toApiResponse();
```

## Resource Enum Output

```php
'status' => [
    'value' => $this->status->getValue(),
    'label' => $this->status->label(),
],
```

## Headers

Read currency and language from validated request headers. Do not trust header values without checking supported currencies/locales.
