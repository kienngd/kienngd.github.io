# Laravel logout other devices


Check file: **app/Http/Kernel.php** (or file **app/Ship/Kernels/HttpKernel.php** if you use Apiato) and uncomment this line:
```php
'web' => [
    // ...
    \Illuminate\Session\Middleware\AuthenticateSession::class,
    // ...
],
```

Logout all other devices:
```php
use Illuminate\Support\Facades\Auth;
...
Auth::logoutOtherDevices($password);
```
<!--more-->
