# Apiato laravel based framework


Home page: http://docs.apiato.io/

**Create project using composer from latest stable**
```bash
composer create-project apiato/apiato apiato9
```
Then edit the .env file.

**Migrate database**
```bash
php artisan migrate
```

**Create admin user, some permissions, roles**
```bash
php artisan db:seed
```
Default account is: admin@admin.com / admin.

**Add all current permissions to admin role.**
```bash
php artisan apiato:permissions:toRole admin
```

**Install OAuth 2.0**
```bash
php artisan passport:install
```
Then edit file **.env** update CLIENT_WEB_ADMIN_ID, CLIENT_WEB_ADMIN_SECRET with the new created value.

**Install ApiDocJs**
```bash
yarn install
```

**Create api doc**
```bash
php artisan apiato:apidoc
```
Your default document url is: http://<Your domain>/api/documentation and http://<Your domain>/api/private/documentation

Default result is saved in: **public/api/documentation/**
<!--more-->
**Testing setup**

Edit file: phpunit.xml, update API_FULL_URL, DB_CONNECTION, DB_DATABASE

**Run the test**
```bash
vendor/bin/phpunit
```

