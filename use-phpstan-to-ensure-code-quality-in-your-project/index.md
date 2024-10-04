# Use PHPStan to Ensure Code Quality in Your Project


![PHPStan A Testing Tool](phpstan-banner.png "PHPStan A Testing Tool")

## **Introduction**

**PHPStan** is a powerful static analysis tool for PHP that checks your code for potential errors without executing it. By using **PHPStan**, you can catch bugs early in the development process, improve the overall **quality** of your code, and ensure your project is more **stable** and **maintainable**.

<!--more-->

## **Installation**

You can install **PHPStan** via **Composer** by run the following command in your project’s root directory:

```bash
composer require --dev phpstan/phpstan
```

Alternatively, if you prefer not to use composer, you can download the **phar file** directly from [PHPStan’s official github](https://github.com/phpstan/phpstan/releases) and use that to run the tool.

## **Basic Usage**

Once **PHPStan** is installed, you can start analyzing your codebase with a simple command. Assuming your code is located in a folder called `src-folder`, use the following command:

```bash
vendor/bin/phpstan analyse src-folder
```

This will trigger **PHPStan** to scan the directory for potential issues and report any problems it finds. If there are errors or warnings, **PHPStan** will display them in the console, helping you identify where the issues are.

You can find more options from [PHPStan document site](https://phpstan.org/user-guide/command-line-usage)

## **Configuration**

To customize how **PHPStan** analyzes your project, you can create a configuration file called **`phpstan.neon`**. This file allows you to adjust various settings, such as the strictness of the analysis or which directories to scan.

Here’s a simple example of a `phpstan.neon` file:

```neon
parameters:
    level: 5
    paths:
        - src
```

- `level`: Specifies the analysis level from 0 (basic checks) to 9 (the strictest). You can start at a lower level and gradually increase it as your project evolves.
- `paths`: Defines the directory or directories **PHPStan** should analyze. In this example, it checks the `src` folder.

You can find more options from [PHPStan document site](https://phpstan.org/config-reference)

## **Advanced Features**

**PHPStan** offers a range of advanced features to help you get the most out of your static analysis.

1. **Increasing Analysis Levels**: As your project grows and your code becomes more complex, you can increase the analysis level to catch more subtle issues. For example, to run **PHPStan** at the highest level, use:

    ```bash
    vendor/bin/phpstan analyse --level max src
    ```

2. **CI/CD Integration**: **PHPStan** can be integrated into your Continuous Integration/Continuous Deployment (CI/CD) pipeline. By adding **PHPStan** checks to your CI/CD process, you can ensure that code quality is maintained before any new code is merged or deployed. This helps catch potential issues early and reduces the risk of introducing bugs into production.

## **Conclusion**

**PHPStan** is a valuable tool for any PHP developer looking to improve code quality and reduce bugs. By integrating **PHPStan** into your development workflow, you can catch issues early, maintain high-quality code, and ultimately create more reliable and maintainable applications.

Start using **PHPStan** today and experience the benefits of static analysis firsthand!
