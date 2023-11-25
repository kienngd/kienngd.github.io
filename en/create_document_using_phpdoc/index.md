# Create document using phpdoc

Hello. In this post, we will learn how to build document using phpdoc. Have fun!

1. Install phpdoc

    **Using composer**

    ```bash
    composer require "phpdocumentor/phpdocumentor:2.*"
    ```

    Then run command

    ```bash
    vendor/bin/phpdoc ...
    ```

    **Manual**: Download file phar from: [Github releases](https://github.com/phpDocumentor/phpDocumentor/releases)

    Then run command

    ```bash
    php phpDocumentor.phar ...
    ```
<!--more-->
2. Some simple commands

    ```bash
    vendor/bin/phpdoc template:list
    vendor/bin/phpdoc run -d SRC -t DEST --template=TEMPLATE_NAME
    ```

3. ...

