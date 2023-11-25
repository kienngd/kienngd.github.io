# Add new guard to an Apiato11 project


<!--more-->
## Edit config
- `config/auth.php` section `guards` and `providers`
  ```php {hl_lines=["4-7"]}
    // ...
    'guards' => [
      // ...
      'web_custom_guard' => [
            'driver' => 'session',
            'provider' => 'custom_guard',
        ],
      // ...
    ]
    // ...
    'providers' => [
      // ...
      'custom_guard' => [
            'driver' => 'eloquent',
            'model' => 'CUSTOM_CLASS',
        ],
      // ...
    ]
    // ...
  ```

## Task 
- LoginTask

    ```php
    //...
    Auth::guard('web_custom_guard')->attempt(...)
    //...
    ```
- LogoutTask
  ```php
    //...
    Auth::guard('web_custom_guard')->logout();
    //...
  ```

## Handle UnAuthenticationException
- `app/Ship/Exceptions/Handlers/ExceptionsHandler.php`
  ```php
    //...
    protected function unauthenticated($request, LaravelAuthenticationException $e): JsonResponse|Response
    {
        if($this->shouldReturnJson($request, $e)) {
            return($this->buildResponse(new CoreAuthenticationException()));
        }
        return(redirect()->guest(route(RouteServiceProvider::getLoginRouteNameFromGuard($e->guards()))));
    }    
  ```
## Get-login-route-name from guard 
- `app/Ship/Providers/RouteServiceProvider.php`
  ```php
    //....
    /** getLoginRouteNameFromGuard */
    public static function getLoginRouteNameFromGuard($guardName) {
        if(is_array($guardName)) {
            $guardName = $guardName[0] ?? null;
        }
        if(!is_string($guardName) || empty($guardName)) {
            return(self::LOGIN);
        }
        switch($guardName) {
            case 'web_custom_guard':
                return(self::WEB_CUSTOM_LOGIN);

            default: 
                return(self::LOGIN);
        }
    }
  ```

