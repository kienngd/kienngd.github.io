# Introduction to PHPDocumentor


![PHPDocumentor](phpdocumentor.png "PHPDocumentor")

`PHPDocumentor` is a tool that helps generate `technical documentation` for `PHP projects`. It reads your PHP code and creates detailed documentation for `functions`, `classes`, and `methods`... This is useful for both new developers and teams working together.

## Why Use PHPDocumentor?

Using PHPDocumentor makes it easier to understand and maintain your code. It helps others quickly see how to use your functions and classes. Good documentation can save time and reduce mistakes. Also, it improves the quality of your project by keeping everything organized.
<!--more-->

## How to Install and Run PHPDocumentor

One easy way to install PHPDocumentor is by downloading the `.phar` file. This is a standalone file that contains everything you need.

1. Download the `.phar` file from the [phpDocumentor github website](https://github.com/phpDocumentor/phpDocumentor/releases).
2. Run the file using the command line to generate the documentation for your project:

```bash
php phpDocumentor.phar -d SOURCE-FOLDER -t TARGET-FOLDER
```
phpDocumentor needs at least a `SOURCE-FOLDER` to scan, (via argument or have this information in a configuration file). If you omit the `TARGET-FOLDER` then your documentation will be generated in a subfolder, of your current working directory, called `.phpdoc/build/`.

### Why Not Use Composer?

You can install `phpDocumentor` with Composer, but it's not the best option. PHPDocumentor has many libraries that are also used by other tools. This can cause conflicts with your project's dependencies. Using the `.phar` file is a simpler and safer choice.


## Basic Command Options

When running PHPDocumentor, there are several options you can use:

- `-d, --directory`: Specifies the directory where your source code is located.
- `-t, --target`: Defines the directory where the documentation will be saved.
- `--template`: Selects a template for the documentation format.

For example:

```bash
php phpDocumentor.phar -d src/ -t docs/
```

This command will generate documentation from the `src/` folder and save it in the `docs/` folder.

## Writing PHP Doc Blocks

To get the best out of PHPDocumentor, add php-doc-blocks to your code. These are special comments that describe each class, function, or method. They help PHPDocumentor create detailed documentation. Here’s an example:

```php
/**
 * Adds two numbers together.
 *
 * @param int $a The first number.
 * @param int $b The second number.
 * @return int The sum of the two numbers.
 */
function add($a, $b) {
    return $a + $b;
}
```

 You can see more details at [PHP-DOC-BLOCK](https://docs.phpdoc.org/guide/guides/docblocks.html#more-on-docblocks).

## Conclusion

Using PHPDocumentor is a great way to create clear and useful documentation for your PHP project. By using the `.phar` file, you can avoid adding extra dependencies. Make sure to use good php-doc-blocks to get the best results. Happy coding!

