---
title: php-late-static-binding
date: 30/05/2023
tags: php static-binding oop
---

# **php-late-static-binding** 202305302229 
> **c67b0b**

Late static binding resolves at runtime instead of compile time.

```php
class A {
    public static string $alfa = 'A';
    public static function getAlfa() : string{
        retrun static::$alfa; #late static binding
    }
}

class B extends A {
    public static string $alfa = 'B';
}

# call from main
echo B::getAlfa(); // resolves to B
echo A::getAlfa(); // resolves to A
```
