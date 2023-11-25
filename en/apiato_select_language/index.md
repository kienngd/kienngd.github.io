# Apiato select language


Hello, today we will learn how to add select language to an ApiAto web app. Have fun!

Document: https://docs.apiato.io/features/localization/

<u>Step 1</u>: Add new language to supported language:

Edit **supported_languages** inside file **app/Containers/Localization/Configs/localization.php**<!--more-->

<u>Step 2</u>: Check **default language** and **fall back language** inside file **config/app.php**

<u>Step 3</u>: Define a localization string inside file **app/Containers/[Container]/Resources/Languages/[language name]/[file name].php**

<u>Step 4</u>: Get a localization string inside your code (controller, blade...): **trans('[container]::[filename].[string_key]')** or **{{ __('[container]::[filename].[string_key]') }}**, **@lang('[container]::[filename].[string_key]')** ...

Example:  
- Language file: **app/Containers/Store/Resources/Languages/en/messages.php**
- Content:
```php
<?php

return [
    'welcome' => 'Welcome to My Store',
];
```
- Then inside your blade view **{{ __('store::messages.welcome') }}**

<u>Step 5</u>: Define a route to set language
```php
$router->get('lang/{locale}', function($locale) {
    App::setLocale($locale);
    session()->put('locale', $locale);    
    return(redirect('/'));
});
```

<u>Step 6</u>: Edit your midleware to get language from session
File: **app/Containers/Localization/Middlewares/LocalizationMiddleware.php**
Function: **findLanguage**
```php
...
private function findLanguage($request)
    {
        ...
        if( session()->get('locale') ) {
            $language = session()->get('locale');
        }

        return $language;
    }
```
System will get language (and overwrite) from: locale from config file, Accept-Language header, locale from session

