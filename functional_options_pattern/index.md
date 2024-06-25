# Functional options pattern with example


## What is the Functional Options Pattern?

The Functional Options Pattern is a design pattern used in programming. It helps to set up options for a function or object in a flexible and clear way. Instead of having many parameters in a function, you use options to configure it.

<!--more-->

## When to Use the Functional Options Pattern

**Use this pattern when**:
- You have a function with many optional parameters.
- You want to make your code easier to read.
- You need to add new options in the future without changing existing code.

## Benefits and Drawbacks of the Functional Options Pattern

### Benefits:
- **Readability**: Your code is cleaner and easier to understand.
- **Flexibility**: You can easily add or remove options.
- **Maintainability**: Future changes are simpler and safer.

### Drawbacks:
- **Complexity**: The pattern can be complex to implement and understand.
- **Performance**: There might be a small performance overhead.

## Example in Go (Golang)

Here’s a simple example to illustrate the Functional Options Pattern in Go:

```go
package main

import "fmt"

// Options struct to hold the options
type Options struct {
    Timeout   int
    MaxRetries int
}

// Default values for options
var defaultOptions = Options{
    Timeout:   30,
    MaxRetries: 3,
}

// Option function type
type Option func(*Options)

// Function to set timeout option
func WithTimeout(timeout int) Option {
    return func(o *Options) {
        o.Timeout = timeout
    }
}

// Function to set max retries option
func WithMaxRetries(maxRetries int) Option {
    return func(o *Options) {
        o.MaxRetries = maxRetries
    }
}

// Function that uses the options
func Connect(addr string, opts ...Option) {
    // Initialize options with default values
    options := defaultOptions
    // Apply each option to the options struct
    for _, opt := range opts {
        opt(&options)
    }

    // Use the options in your function
    fmt.Printf("Connecting to %s with timeout %d and max retries %d\n", addr, options.Timeout, options.MaxRetries)
}

func main() {
    // Connect with default options
    Connect("example.com")

    // Connect with custom timeout
    Connect("example.com", WithTimeout(60))

    // Connect with custom timeout and max retries
    Connect("example.com", WithTimeout(60), WithMaxRetries(5))
}
```

## Example in PHP

Here’s a simple example to illustrate the Functional Options Pattern in PHP:

```php
<?php

class Options {
    public $timeout;
    public $maxRetries;

    public function __construct($timeout = 30, $maxRetries = 3) {
        $this->timeout = $timeout;
        $this->maxRetries = $maxRetries;
    }
}

function withTimeout($timeout) {
    return function($options) use ($timeout) {
        $options->timeout = $timeout;
    };
}

function withMaxRetries($maxRetries) {
    return function($options) use ($maxRetries) {
        $options->maxRetries = $maxRetries;
    };
}

function connect($addr, ...$opts) {
    $options = new Options();
    
    foreach ($opts as $opt) {
        $opt($options);
    }

    echo "Connecting to $addr with timeout {$options->timeout} and max retries {$options->maxRetries}\n";
}

// Connect with default options
connect("example.com");

// Connect with custom timeout
connect("example.com", withTimeout(60));

// Connect with custom timeout and max retries
connect("example.com", withTimeout(60), withMaxRetries(5));
?>
```

## Conclusion

The Functional Options Pattern is a powerful tool for making your code more flexible and easier to read. It helps to manage complex configurations in a clean way. However, it can also add complexity and a small performance cost. Use it wisely to get the most benefits.

