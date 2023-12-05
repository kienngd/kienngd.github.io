# Quick-notes: working with Laravel


<!--more-->
# Some Quick-notes

## Laravel
- Encrypt / Decrypt message with Laravel 10
  ```php
  use Illuminate\Support\Facades\Crypt;
  $encrypted = Crypt::encrypt('My secret message');
  $decrypted = Crypt::decrypt($encrypted);
  // -- OR --
  $encrypted = Crypt::encrypt('My secret message', 'secret_key');
  $decrypted = Crypt::decrypt($encrypted, 'secret_key');
  ```
  - config('app.cipher') is encrypt / decrypt algorithm
  - config('app.key') is default secret_key

## Funcional test
- Set domain / host when test
```php
public function testUriWithFakeDomain($uri) {
    // ...
    \URL::forceRootUrl('https://url.com');
    // Or
    request()->headers->set('url.com');
    $response = $this->get($uri);
    // ...
}

```

## APIATO - Nova3
- Register policy in file: `app/Containers/Authentication/Providers/AuthProvider.php`

## Install StanclTenancy
- Document: https://tenancyforlaravel.com/docs/v3/quickstart
- Quick start:
  - Create a laravel project: `composer create-project laravel/laravel stancltenancy.localserver.test`
  - Config nginx, edit hosts file.
  - Install package: 
    ```bash
    composer require stancl/tenancy
    php artisan tenancy:install
    ```
  - Edit database config in .env and config/database.php
  - Check migration-files
  - Run migrate: `php artisan migrate`
  - Register service provider: `config/app.php`
    ```php
    ....
    App\Providers\EventServiceProvider::class,
    App\Providers\RouteServiceProvider::class,
    App\Providers\TenancyServiceProvider::class, // <-- Add this provider
    ....
    ```
  - Create a tenant model extends from `Stancl\Tenancy\Database\Models\Tenant` implements `Stancl\Tenancy\Contracts\TenantWithDatabase` uses traits `Stancl\Tenancy\Database\Concerns\HasDatabase` and `Stancl\Tenancy\Database\Concerns\HasDomains`
    ```php
      <?php
        namespace App\Models;

        use Stancl\Tenancy\Database\Models\Tenant as BaseTenant;
        use Stancl\Tenancy\Contracts\TenantWithDatabase;
        use Stancl\Tenancy\Database\Concerns\HasDatabase;
        use Stancl\Tenancy\Database\Concerns\HasDomains;

        class Tenant extends BaseTenant implements TenantWithDatabase
        {
            use HasDatabase, HasDomains;
        }
    
    ```
  - Edit `config/tenancy.php`
    ```php
      'tenant_model' => \App\Models\Tenant::class, // <-- Your class here
    ```
  - When you create a new tenant, it will run `CreateDatabase`, `MigrateDatabase` and optional `SeedDatabase`
  - Set central-routes `app/Providers/RouteServiceProvider.php`
    ```php
      public function boot()
      {
          // ...

          $this->routes(function () { // <-- Change these lines
              $this->mapApiRoutes();
              $this->mapWebRoutes();
          });
      }
      // <-- Add these lines
      protected function mapWebRoutes()
      {
          foreach ($this->centralDomains() as $domain) {
              Route::middleware('web')
                  ->domain($domain)
                  ->namespace($this->namespace)
                  ->group(base_path('routes/web.php'));
          }
      }

      protected function mapApiRoutes()
      {
          foreach ($this->centralDomains() as $domain) {
              Route::prefix('api')
                  ->domain($domain)
                  ->middleware('api')
                  ->namespace($this->namespace)
                  ->group(base_path('routes/api.php'));
          }
      }

      protected function centralDomains(): array
      {
          return config('tenancy.central_domains');
      }
    ```
  - Tenant routes in file: `routes/tenant.php`
  - Migrations: Copy migration-files to: `database/migrations/tenant`. When a tenant is created, it will run these migration-files
  - Creating tenants
    ```php tinker
      $tenant1 = App\Models\Tenant::create(['id' => 'tenant1']);
      $tenant1->domains()->create(['domain' => 'tenant1.localhost']);

      $tenant2 = App\Models\Tenant::create(['id' => 'tenant2']);
      $tenant2->domains()->create(['domain' => 'tenant2.localhost']);
    ```
    Database will be created automatically when you create tenant
  - Create a user inside each tenant's database:
    ```php tinker
      App\Models\Tenant::all()->runForEach(function () {
        App\Models\User::factory()->create();
      });
    ```
  - Trying it out: Access each central-domain, you will see the laravel default homepage. Access your each tenant-domain, you will see default tenant's homepage

- Need to do:
  - APIATO with StanclTenancy
    - Migration path.

## Laravel backpack 6
- Document: https://backpackforlaravel.com/docs/6.x/installation
- Install laravel 10: `composer create-project laravel/laravel backpack6.localserver.test`
- Edit file `.env`
- Install backpack: `composer require backpack/crud`. You need to curl your site to finish install.
- Install some backpack add-ons
- Create a CRUD for each model: `php artisan backpack:crud {model}`
- Or create CRUD for all model: `php artisan backpack:build`
- Need to do:
  - APIATO, StanclTenancy, BackPack work together.

