# Quick-notes


<!--more-->
# Some Quick-notes

## PostgreSQL
- Get all running query
  ```sql
    SELECT pid, state, query, age(clock_timestamp(), query_start) AS query_age, psa.*
    FROM pg_stat_activity psa
  ```
- Miscellaneous
  ```bash
    pg_lsclusters
    sudo pg_dropcluster 14 main --stop
    sudo pg_upgradecluster 12 main    
  ```

## Sqlite3
- Install sqlite3-console ubuntu: `sudo apt install sqlite3`
- Connect to db file: `sqlite3 path/to/db/file`

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

## Install awscli
  ```bash
    sudo apt update
    sudo apt install awscli
    aws --version
    aws configure
    aws configure [--profile profile-name]
    aws configure set region us-west-2 --profile profile1
    aws configure list
    aws help
    aws s3 help
    aws s3 rm help
    aws --endpoint-url=https://s3south.storage.com.vn --profile citigo1 s3 ls
    aws --endpoint-url=https://s3south.storage.com.vn --profile citigo1 s3 rm --recursive s3://kiotviet-export
    aws --endpoint-url=https://s3south.storage.com.vn --profile citigo2 s3 rm --recursive s3://kiotvietimages
  ```
  **aws params**
  ```
    --endpoint-url
    --no-verify-ssl
    --no-paginate
    --output : json / text / table
    --profile : 
    --color : on / off / auto
    --cli-read-timeout
    --cli-connect-timeout

  ```

## Ubuntu
- Show OS version-information
  ```bash
    lsb_release -a
  ```
- Add self-signed CA
  - copy file rootCA.crt to `/usr/local/share/ca-certificates`
  - Update: `sudo update-ca-certificates`  
  - Convert pem to crt in **der-format** `openssl x509 -outform der -in yourfile.pem -out yourfile.crt`
  - Convert perm to crt in **ASCII-PEM-format** just rename.
- ....

## Openbox
- Openbox configuration-file: `~/.config/openbox/rc.xml`
- Reload configuration-file (after edit): `openbox --reconfigure`

## Linux commands
- List folder, short desc by size: du -sh database/backup/* | sort -hr

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

## GIT commands
- Update branches-list (and other information): `git fetch --prune origin`
- Delete remote branches: `git push origin --delete branch_1 branch_2` or `git push origin :branch_1 :branch_2`
- List all remote branches: `git branch -r`
