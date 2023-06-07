---
title: php-autoloading
date: 06/06/2023
tags: php autoloading
---

# **php-autoloading** 202306062216 
> **4a6b01**

  

## Autoloading

using spl_autoload_register

```php
<?php
/**
 * Simple autoloader
 *
 * @param $class_name - String name for the class that is trying to be loaded.
 */
function my_custom_autoloader( $class_name ){
    $file = __DIR__.'/includes/'.$class_name.'.php';

    if ( file_exists($file) ) {
        require_once $file;
    }
}

// add a new autoloader by passing a callable into spl_autoload_register()
spl_autoload_register( 'my_custom_autoloader' );

$my_example = new SomeClass1(); // this works!
```

## Autoloading with namespaces

- Declare an autoloading class
```php
<?php


class Autoloader
{
    public static function ClassLoader(string $className)
    {
        $class_path = str_replace('\\', '/', $className);

        $filePath = dirname(__DIR__, 1) . "/$class_path.php";
            

        // var_dump($filePath);

        
            if (file_exists($filePath)) {
                // echo $filePath . '<br>';
                require $filePath;
            }
        
    }
}

spl_autoload_register('Autoloader::ClassLoader');
```

- namespaces and filenames must match
```php
<?php

namespace app\classes;

class Home{

    public function index() : void
    {
        echo 'Home';
    }

}
```

- in index.php

```php
<?php
require_once __DIR__ . '/../app/autoloader.php';

use app\classes\Home;
use app\classes\Invoice;
use app\classes\Router;

//...
```
