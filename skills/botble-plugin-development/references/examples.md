# Botble Plugin Examples

## Model

```php
use Botble\Base\Casts\SafeContent;
use Botble\Base\Models\BaseModel;

class Review extends BaseModel
{
    protected $table = 'plugin_reviews';

    protected $fillable = [
        'name',
        'comment',
        'status',
    ];

    protected function casts(): array
    {
        return [
            'name' => SafeContent::class,
            'comment' => SafeContent::class,
            'status' => ReviewStatusEnum::class,
        ];
    }
}
```

## Form

```php
use Botble\Base\Forms\FormAbstract;
use Botble\Base\Forms\Fields\EditorField;
use Botble\Base\Forms\Fields\MediaImageField;
use Botble\Base\Forms\Fields\SelectField;
use Botble\Base\Forms\Fields\TextField;
use Botble\Base\Forms\FieldOptions\EditorFieldOption;
use Botble\Base\Forms\FieldOptions\MediaImageFieldOption;
use Botble\Base\Forms\FieldOptions\NameFieldOption;
use Botble\Base\Forms\FieldOptions\StatusFieldOption;

class ReviewForm extends FormAbstract
{
    public function setup(): void
    {
        $this
            ->setupModel(new Review())
            ->setValidatorClass(ReviewRequest::class)
            ->columns(12)
            ->add('name', TextField::class, NameFieldOption::make()->colspan(8)->required()->toArray())
            ->add('status', SelectField::class, StatusFieldOption::make()->colspan(4)->toArray())
            ->add('comment', EditorField::class, EditorFieldOption::make()->label(trans('plugins/reviews::reviews.comment')))
            ->add('image', MediaImageField::class, MediaImageFieldOption::make()->label(trans('core/base::forms.image')));
    }
}
```

## Table

```php
use Botble\Table\Columns\CreatedAtColumn;
use Botble\Table\Columns\FormattedColumn;
use Botble\Table\Columns\IdColumn;
use Botble\Table\Columns\NameColumn;
use Botble\Table\Columns\StatusColumn;

$this
    ->model(Review::class)
    ->addColumns([
        IdColumn::make(),
        NameColumn::make()->route('reviews.edit'),
        FormattedColumn::make('rating')
            ->formatted(fn ($value) => number_format((float) $value, 1)),
        StatusColumn::make(),
        CreatedAtColumn::make(),
    ]);
```

## Service Provider

```php
use Botble\Base\Supports\ServiceProvider;
use Botble\Base\Facades\DashboardMenu;

class ReviewsServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        $this
            ->setNamespace('plugins/reviews')
            ->loadAndPublishConfigurations(['permissions'])
            ->loadAndPublishViews()
            ->loadAndPublishTranslations()
            ->loadRoutes()
            ->loadMigrations()
            ->publishAssets();

        DashboardMenu::default()->beforeRetrieving(function (): void {
            DashboardMenu::make()->registerItem([
                'id' => 'cms-plugins-reviews',
                'priority' => 5,
                'name' => trans('plugins/reviews::reviews.name'),
                'icon' => 'ti ti-star',
                'url' => route('reviews.index'),
                'permissions' => ['reviews.index'],
            ]);
        });
    }
}
```

## Admin Routes

```php
use Botble\Base\Facades\AdminHelper;
use Illuminate\Support\Facades\Route;

AdminHelper::registerRoutes(function (): void {
    Route::group(['prefix' => 'reviews', 'as' => 'reviews.'], function (): void {
        Route::resource('', ReviewController::class)
            ->parameters(['' => 'review'])
            ->except(['show']);
    });
});
```

Use `wherePrimaryKey()` on custom `{id}` routes.
