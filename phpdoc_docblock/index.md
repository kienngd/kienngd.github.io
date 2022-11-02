# Phpdoc docblock

```php
/** This is a single line DocComment. */

/**
 * This is a multi-line DocComment.
 */

/**
 * This is a summary
 *
 * This is a description
 */

/**
 * This is a summary.
 * This is a description
 */
```

**Tags** example: @api, @author, @param, @return...
<!--more-->
```php
<?php
/**
 * I belong to a file. File summary
 * 
 * File description.
 */

/**
 * I belong to a class. Class summary
 * 
 * Class description
 * @author ...
 */
class MyClass
{
    /**
     * I belong to a property. Property summary.
     * Property description
     */
    public $myProperty;

    /**
     * I belong to a method. Method summary.
     * Method description
     * 
     * @author ...
     * @param string $param1 ...
     * @param string $param2 ...
     * @return string ...
     */
    public function myFunction($param1, $param2) {
        return('result');
    }
}
```

**Classes and interfaces**

    - Summary
    - Description
    - The following tags:
        - author
        - copyright
        - package
        - subpackage
        - version

**Properties**

    - Summary
    - Description
    - The following tags:
        - author
        - copyright
        - version
        - var

**Methods**

    - Summary
    - Description
    - The following tags:
        - author
        - copyright
        - version
        - param
        - return
        - throws
