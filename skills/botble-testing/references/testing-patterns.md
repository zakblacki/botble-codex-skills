# Testing Patterns

## Admin Create Test

```php
use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;

class ReviewPluginTest extends TestCase
{
    use RefreshDatabase;

    public function test_can_create_review(): void
    {
        $data = [
            'name' => 'Hydrating Rose Face Cream Review',
            'status' => ReviewStatusEnum::PUBLISHED,
        ];

        $response = $this->loginAs()->post(route('reviews.create'), $data);

        $response->assertRedirect();
        $this->assertDatabaseHas('plugin_reviews', [
            'name' => 'Hydrating Rose Face Cream Review',
        ]);
    }
}
```

## Permission Test

Assert unauthorized users cannot access admin routes. Use the project's existing permission helpers when present instead of inventing new auth setup.

## API Test

Assert the response envelope:

```php
$response->assertJson([
    'error' => false,
    'message' => null,
]);
```
