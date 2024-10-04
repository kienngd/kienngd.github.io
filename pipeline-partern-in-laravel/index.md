# Pipeline-partten in Laravel

In Laravel, the **pipeline pattern** helps you process a series of tasks in a clear and organized way. Instead of handling each step separately, you can use a pipeline to apply multiple actions in sequence.

This pattern is useful when you need to apply several steps to data or an object. For example, you can use a pipeline to handle an order request with steps like validation, and adding data to the order and finally save it to database.

<!--more-->

To use the pipeline in Laravel, you need a class or function that can take and return data. You also define the steps to apply and the order. Laravel provides the `Pipeline` class to help with this.

Here is a basic example of using the pipeline in Laravel:
**Scenario**: You need to apply multiple processing steps to an order: apply a discount, calculate shipping costs, and finalize the order.

## Step 1: Define Pipeline Steps
```php
// ApplyDiscount.php
namespace App\Pipeline;

class ApplyDiscount
{
    public function handle($order, $next)
    {
        if ($order['discount_code'] === 'SUMMER21') {
            $order['total'] -= 10; // Apply a $10 discount
        }
        return $next($order);
    }
}

// CalculateShipping.php
namespace App\Pipeline;

class CalculateShipping
{
    public function handle($order, $next)
    {
        $order['shipping'] = 5; // Flat $5 shipping cost
        $order['total'] += $order['shipping'];
        return $next($order);
    }
}

// FinalizeOrder.php
namespace App\Pipeline;

class FinalizeOrder
{
    public function handle($order, $next)
    {
        // Save the order to the database
        // Order::create($order); // Uncomment to save to DB
        return $order; // Return the final order
    }
}
```

## Step 2: Use the Pipeline
```php
use Illuminate\Pipeline\Pipeline;
use App\Pipeline\ApplyDiscount;
use App\Pipeline\CalculateShipping;
use App\Pipeline\FinalizeOrder;

$order = [
    'item' => 'Laptop',
    'total' => 1000,
    'discount_code' => 'SUMMER21',
];

$processedOrder = app(Pipeline::class)
    ->send($order)
    ->through([
        ApplyDiscount::class,
        CalculateShipping::class,
        FinalizeOrder::class,
    ])
    ->thenReturn();

print_r($processedOrder);

```

**Explanation**:
- ApplyDiscount applies a discount if the code matches.
- CalculateShipping adds shipping costs.
- FinalizeOrder prepares the order for saving.

The pipeline pattern makes your code cleaner and easier to manage. Each step is separate, so it’s easier to understand and update.
