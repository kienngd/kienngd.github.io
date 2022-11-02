# Use UUID as primary key of Laravel Eloquent ORM

Install package using composer:
```bash
composer require goldspecdigital/laravel-eloquent-uuid:^7.0
```

Inside migration file.
```php
// Replace this
$table->increments('id');
// By this
$table->uuid('id')->primary();
```
<!--more-->
Inside model file
```php
use GoldSpecDigital\LaravelEloquentUUID\Database\Eloquent\Uuid;
...
class MyModel extends Model
{
    use Uuid;
    protected $keyType = 'string';
    public $incrementing = false;
    protected $guarded = [];
}
```
