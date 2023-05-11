# Strategy Pattern in PHP with examples

## Example 1: Sort
We need to implement a sorting system that sorts an array of numbers in ascending or descending order

### Without pattern
```php
class Sorter {
    public function bubbleSort(array $arr) {
        // Implementation of Bubble Sort
    }
    
    public function quickSort(array $arr) {
        // Implementation of Quick Sort
    }
    
    public function mergeSort(array $arr) {
        // Implementation of Merge Sort
    }
}

$sorter = new Sorter();
$sortedArr = $sorter->bubbleSort($arr); // or $sorter->quickSort($arr) or $sorter->mergeSort($arr)
```

### With pattern
```php
interface SortingStrategy {
    public function sort(array $arr): array;
}
class BubbleSort implements SortingStrategy {
    public function sort(array $arr): array {
        // Implementation of Bubble Sort
    }
}
class QuickSort implements SortingStrategy {
    public function sort(array $arr): array {
        // Implementation of Quick Sort
    }
}
class MergeSort implements SortingStrategy {
    public function sort(array $arr): array {
        // Implementation of Merge Sort
    }
}
```

```php
class Sorter {
    private $sortingStrategy;
    
    public function __construct(SortingStrategy $sortingStrategy) {
        $this->sortingStrategy = $sortingStrategy;
    }
    
    public function sort(array $arr): array {
        return $this->sortingStrategy->sort($arr);
    }
}
$sorter = new Sorter(new BubbleSort());
$sortedArr = $sorter->sort($arr); // or new Sorter(new QuickSort())->sort($arr) or new Sorter(new MergeSort())->sort($arr)
```

## Example 2: Discount Product
We want to implement the discount system

### Without pattern
```php
class DiscountCalculator {
    public function calculateDiscount(Product $product) {
        if ($product instanceof Book) {
            return $product->getPrice() * 0.1;
        } elseif ($product instanceof Clothing) {
            return $product->getPrice() * 0.2;
        } elseif ($product instanceof Electronics) {
            return $product->getPrice() * 0.3;
        }
    }
}
$discountCalculator = new DiscountCalculator();
$discountedPrice = $product->getPrice() - $discountCalculator->calculateDiscount($product);
```

### With pattern
```php
interface DiscountStrategy {
    public function calculateDiscount(Product $product): float;
}
class BookDiscount implements DiscountStrategy {
    public function calculateDiscount(Product $product): float {
        return $product->getPrice() * 0.1;
    }
}
class ClothingDiscount implements DiscountStrategy {
    public function calculateDiscount(Product $product): float {
        return $product->getPrice() * 0.2;
    }
}
class ElectronicsDiscount implements DiscountStrategy {
    public function calculateDiscount(Product $product): float {
        return $product->getPrice() * 0.3;
    }
}
```

```php
class DiscountCalculator {
    private $discountStrategy;
    
    public function __construct(DiscountStrategy $discountStrategy) {
        $this->discountStrategy = $discountStrategy;
    }
    
    public function calculateDiscount(Product $product): float {
        return $this->discountStrategy->calculateDiscount($product);
    }
}
$discountCalculator = new DiscountCalculator(new BookDiscount());
$discountedPrice = $product->getPrice() - $discountCalculator->calculateDiscount($product);
```

## Best Practices for Implementing Strategy Pattern in PHP:
- Keep the Strategy interface simple and focused on the algorithm’s behavior.
- Use meaningful names for the Concrete Strategies to make the code more readable and maintainable.
- Use dependency injection to provide the Concrete Strategies to the Context class.
- Avoid coupling the Concrete Strategies to the Context class to make the code more flexible and reusable.

