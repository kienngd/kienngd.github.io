# Working with HexaDog Laravel-Themes-Manager


<!--more-->
## What is Laravel-Themes-Magager

Link github: https://github.com/hexadog/laravel-themes-manager

## Install
```bash
    composer require hexadog/laravel-themes-manager
    # Publish the configuration file
    php artisan vendor:publish --provider="Hexadog\ThemesManager\Providers\PackageServiceProvider" --tag=config
    # Publish the view files
    php artisan vendor:publish --provider="Hexadog\ThemesManager\Providers\PackageServiceProvider" --tag=views
```

## Create theme
```bash
    php artisan theme:make
```
By default view is in folder: `themes/VENDOR-NAME/THEME-NAME/resources/views/VIEW-NAME.blade.php`

## Set theme
- You can set theme manually in controller
```php
    // ...
    use Hexadog\ThemesManager\Facades\ThemesManager;
    // ....
    ThemesManager::set('VENDOR-NAME/THEME-NAME');
```
- Or via middleware `app/Ship/Middlewares/SetTheme.php`
```php
<?php
namespace App\Ship\Middlewares;

use Closure;
use Hexadog\ThemesManager\Http\Middleware\ThemeLoader as HexadogThemeLoader;

class SetTheme extends HexadogThemeLoader
{
    public function handle($request, Closure $next, $theme = null)
    {
        $theme = 'kiennd/default';
        // Call parent Middleware handle method
        return parent::handle($request, $next, $theme);
    }
}
```
Kernel `app/Ship/Kernels/HttpKernel.php`
```php
use App\Ship\Middlewares\SetTheme;
// ...
protected $middleware = [
    //...
    SetTheme::class, 
]; 
// ...
```

## Assets
Each theme have its assets (images, stylesheets, javascript, ...) inside its folder. When active theme, this folder is **linked** (use symbolic link) into **public/themes** folder so you can access it publicly
`themes/VENDOR-NAME/THEME-NAME/public/`
```php
    {!! Theme::asset('css/app.min.css') !!}
    {!! theme_asset('css/app.min.css') !!}
    # https://URL/themes/VENDOR-NAME/THEME-NAME/css/app.min.css
```
```php
    {!! Theme::style('css/app.min.css') !!}
    {!! theme_style('css/app.min.css') !!}
    # <link href="https://URL/themes/VENDOR-NAME/THEME-NAME/css/app.min.css">
```
```php
    {!! Theme::script('js/app.min.js') !!}
    {!! theme_script('js/app.min.js') !!}
    # <script src="https://URL/themes/VENDOR-NAME/THEME-NAME/js/app.min.js"></script>
```
```php
    {!! Theme::image('img/logo.png', 'My Theme logo') !!}
    {!! theme_image('img/logo.png', 'My Theme logo') !!}
    # <img src="https://URL/themes/VENDOR-NAME/THEME-NAME/img/logo.png" alt="My Theme logo" />
```

## Overwrite error-views
`themes/VENDOR-NAME/THEME-NAME/resources/views/errors`

## Overwrite package-views
`themes/VENDOR-NAME/THEME-NAME/resources/views/vendor/PACKAGE-NAME`

## Language files
`themes/VENDOR-NAME/THEME-NAME/lang/en/` and use translate under namespace `theme`. Example: `__('theme::string.hello')`.

## Composed components
- Page title, theme asset, theme image, theme script, theme style
```html
    <x-theme-page-title title="Home" /> 
    <!-- <title>Home - AppName</title> -->
    <x-theme-page-title title="Home" withAppName=false >
    <!-- <title>Home</title> -->
    <x-theme-page-title title="Home" separator="|" />
    <!-- <title>Home | AppName</title> -->
    <x-theme-page-title title="Home" invert=true >
    <!-- <title>AppName - Home</title> -->
    <x-theme-asset source="css/app.css"/>
    <!-- https://URL/themes/VENDOR-NAME/THEME-NAME/css/app.css -->
    <x-theme-image source="img/logo.png"/> 
    <!-- <img src="https://URL/themes/VENDOR-NAME/THEME-NAME/img/logo.png" /> -->
    <x-theme-image source="img/logo.png" class="image" alt="Logo" />
    <!-- <img src="themes/VENDOR-NAME/THEME-NAME/img/logo.png" class="image" alt="logo" /> -->
    <x-theme-style source="css/app.css"/>
    <!-- <link src="https://URL/themes/VENDOR-NAME/THEME-NAME/css/app.css" rel="stylehseet"> -->
    <x-theme-style source="css/app.css" media="print"/>
    <!-- <link src="https://URL/themes/VENDOR-NAME/THEME-NAME/css/app.css" rel="stylehseet" media="print"> -->

```

## Configurations
- Themes directory: `themes-manager.diretory` default is themes
- Public assets: `themes-manager.symlink_path` default is public
- Fallback theme: `themes-manager.fallback_theme`
- Cache: `themes-manager.cache.enabled`, `themes-manager.cache.lifetime`, `themes-manager.cache.key`


## Artisan commands
- `php artisan theme:make`
- `php artisan theme:list`
- `php artisan theme:activate hexadog/default`
- `php artisan theme:deactivate hexadog/default`
- `php artisan theme:cache`
- `php artisan theme:cache:clear`
