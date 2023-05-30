---
title: php-oop-polymorphism
date: 30/05/2023
tags: php oop polymorphism
---

# **php-oop-polymorphism** 202305301513 
> **7260db**

  

## Example using interfaces

```php
// ICollectable interface
<?php

namespace App;
interface ICollectable {
    public function collect(int $owedAmount) : void;
}

// Private collector class
<?php

namespace App;

use App\ICollectable;



class PrivateCollector implements ICollectable{

    public function collect(int $owedAmount): void {
        $amount = $owedAmount * 0.65;
        echo 'Private collector collected: ' . $amount . ' out of ' . mt_rand((int)$amount, (int)$owedAmount) . PHP_EOL;
    }

}

// Collector Service Agency class
<?php

namespace App;
class CollectingServiceAgency implements ICollectable {
    function __construct(){

    }

    public function collect(int $owedAmount): void {
        $amount = $owedAmount * 0.5;
        echo 'Collecting services collected ' . mt_rand((int)$amount, (int)$owedAmount) . ' out of ' . $owedAmount . PHP_EOL;        
    }
}

// Debt Collection service
<?php

namespace App;

use App\ICollectable;

class DebtCollectionService {

    public function collectDebt(ICollectable $collector, int $owedAmount): void{
        $collector->collect($owedAmount);
    }

}

// index.php
<?php
declare(strict_types=1);


use App\CollectingServiceAgency;
use App\DebtCollectionService;
use App\PrivateCollector;

require __DIR__ . '/../vendor/autoload.php';

$collector = new DebtCollectionService();
print $collector->collectDebt(new CollectingServiceAgency(), mt_rand(100, 1000));
echo $collector->collectDebt(new PrivateCollector(), mt_rand(100, 1000));
```
