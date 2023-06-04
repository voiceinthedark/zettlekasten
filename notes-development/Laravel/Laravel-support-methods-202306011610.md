---
title: Laravel-support-methods
date: 01/06/2023
tags: php laravel
---

# **Laravel-support-methods** 202306011611 
> **f8cc3a**

  

## Support Methods

### Collection

```php
$collection = collect(['taylor', 'abigail', null])->map(function (string $name) {
    return strtoupper($name);
})->reject(function (string $name) {
    return empty($name);
});
```

#### Extending collection

```php
use Illuminate\Support\Collection;
use Illuminate\Support\Str;
 
Collection::macro('toUpper', function () {
    return $this->map(function (string $value) {
        return Str::upper($value);
    });
});
 
$collection = collect(['first', 'second']);
 
$upper = $collection->toUpper();
 
// ['FIRST', 'SECOND']
```

Typically, you should declare collection macros in the boot method of a service provider.

### Collection Methods

- join:
  ```php
  collect(['a', 'b', 'c'])->join(', '); // 'a, b, c'
  collect(['a', 'b', 'c'])->join(', ', ', and '); // 'a, b, and c'
  collect(['a', 'b'])->join(', ', ' and '); // 'a and b'
  collect(['a'])->join(', ', ' and '); // 'a'
  collect([])->join(', ', ' and '); // ''
  ```
- collapse: 
    The collapse method collapses a collection of arrays into a single, flat collection:
  ```php
    $collection = collect([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
    ]);
 
    $collapsed = $collection->collapse();
 
    $collapsed->all();
 
    // [1, 2, 3, 4, 5, 6, 7, 8, 9]
  ```

- partition:
     The partition method may be combined with PHP array destructuring to separate elements that pass a given truth test from those that do not:
    ```php
      $collection = collect([1, 2, 3, 4, 5, 6]);
   
      [$underThree, $equalOrAboveThree] = $collection->partition(function (int $i) {
      return $i < 3;
      });
   
      $underThree->all();
   
      // [1, 2]
   
      $equalOrAboveThree->all();
   
      // [3, 4, 5, 6]
    ```
- unique
 The unique method returns all of the unique items in the collection. The returned collection keeps the original array keys, so in the following example we will use the values method to reset the keys to consecutively numbered indexes:
  ```php
    $collection = collect([1, 1, 2, 2, 3, 4, 2]);
   
  $unique = $collection->unique();
   
  $unique->values()->all();
   
  // [1, 2, 3, 4]  

      $collection = collect([
        ['name' => 'iPhone 6', 'brand' => 'Apple', 'type' => 'phone'],
        ['name' => 'iPhone 5', 'brand' => 'Apple', 'type' => 'phone'],
        ['name' => 'Apple Watch', 'brand' => 'Apple', 'type' => 'watch'],
        ['name' => 'Galaxy S6', 'brand' => 'Samsung', 'type' => 'phone'],
        ['name' => 'Galaxy Gear', 'brand' => 'Samsung', 'type' => 'watch'],
    ]);
     
    $unique = $collection->unique('brand');
     
    $unique->values()->all();
     
    /*
        [
            ['name' => 'iPhone 6', 'brand' => 'Apple', 'type' => 'phone'],
            ['name' => 'Galaxy S6', 'brand' => 'Samsung', 'type' => 'phone'],
        ]
    */
  ```
