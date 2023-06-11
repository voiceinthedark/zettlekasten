---
title: php-oop-classes
date: 28/05/2023
tags: php oop property magic-methods
---

# **php-oop-classes** 202305282257 
> **a9d984**

  
### Property promotion

By supplying the properties directly in the constructor, php will automatically
provide the fields implementation.

```PHP
class Customer{
    public function __construct(
        private string $name,
        private int $age
    ) {}

    public function getName(){
        return $this->name;
    }

    public function getAge(){
        return $this->age;
    }

}
```

### Magic methods

#### \_\_call() method

This magic method act as a wrapper around a class function that doesn't exist.
inside the function we then can call the non-class method as if it's class method.

```php
class Customer{
    public function __construct(
        private string $name,
    )
    
    public function __call($name, $arguments){
        return call_user_func_array([$this, $name], $arguments);
    }
}
```

The `__call()` method accepts two arguments:

-   `$name` is the name of the method that is being called by the object.
-   `$arguments` is an array of arguments passed to the method call.

The `__call()` method is useful when you want to create a wrapper class that wraps the existing API.

##### \_\_call() method example
Suppose that you want to develop the `Str` class that wraps existing string functions such as `strlen()`, `strtoupp()`, `strtolower()`, etc.

Typically, you can define the method explicitly like length, upper, lower, … But you can use utilize the `__call()` magic method to make the code shorter.

The following defines the Str class that uses the `__call()` magic method:

```php
<?php

class Str
{
private $s = '';

private $functions = [
'length' => 'strlen',
'upper' => 'strtoupper',
'lower' => 'strtolower'
// map more method to functions
];

public function __construct(string $s)
{
$this->s = $s;
}

public function __call($method, $args)
{
if (!in_array($method, array_keys($this->functions))) {
throw new BadMethodCallException();
}

array_unshift($args, $this->s);

return call_user_func_array($this->functions[$method], $args);
}
}
```
The `$functions` property store the mapping between the methods and built-in string function. For example, if you call the `length()` method, the `__call()` method will call the `strlen()` function.

When you call a method on an object of the Str class and that method doesn’t exist e.g., `length()`, PHP will invoke the `__call()` method.

The `__call()` method will raise a `BadMethodCallException` if the method is not supported. Otherwise, it’ll add the string to the argument list before calling the corresponding function.