---
title: php-oop-classes
date: 28/05/2023
tags: php oop property
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
