# PHP "pass by value" VS "pass by reference"

Hello, it is me again. Today, we will talk about "**pass by value**" or "**pass by reference**". I use PHP 7.4 and Ubuntu 20.04 to test. Happy coding!

We have an example class:
```php
class MyClass {
   public $x;
   public $y;
 
   public function __construct($x, $y) {
       $this->x = $x;
       $this->y = $y;
   }
 
   public function setX($x)
   {
       $this->x = $x;
   }
 
   public function setY($y)
   {
       $this->y = $y;
   }
}
```
<!--more-->
And two functions:
```php
function TestByValueFunc($myClass) {
   $myClass->setX(8);
   $myClass = new MyClass(6, 7);
}

function TestByRefueFunc(&$myClass) {
   $myClass->setX(8);
   $myClass = new MyClass(6, 7);
}
```

Then we can test the output
```php
$myClass = new MyClass(4, 5);
echo $myClass->x, '    ', $myClass->y, PHP_EOL;
TestByValueFunc($myClass);
echo $myClass->x, '    ', $myClass->y, PHP_EOL;
TestByRefueFunc($myClass);
echo $myClass->x, '    ', $myClass->y, PHP_EOL;
```

The result will be:
```console
4    5
8    5
6    7
```

Could you please explain why the result is like this?

