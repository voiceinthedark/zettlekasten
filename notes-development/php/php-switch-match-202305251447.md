---
title: php-switch-match
date: 25/05/2023
tags: php switch match
---

# **php-switch-match** 202305251447 
> **d3ffbe**

  

### Matching
Same as switch but in compact form
```php
<?php
$food = 'cake';

$return_value = match ($food) {
    'apple' => 'This food is an apple',
    'bar' => 'This food is a bar',
    'cake' => 'This food is a cake',
};

var_dump($return_value);
?>
```
