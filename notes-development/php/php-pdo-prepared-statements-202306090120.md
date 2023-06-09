---
title: php-pdo-prepared-statements
date: 09/06/2023
tags: php pdo database sql-injections
---

# **php-pdo-prepared-statements** 202306090120 
> **3af9d2**

  
## PDO prepared statements

In order to optimize queries and protect against malicious sql injections, prepared 
statements are a must.

```php
try {

            $id = 15;
            // open pdo connection to my_db database that runs on a docker container
            $db = new PDO('mysql:host=db;dbname=my_db', 'root', 'root', [
                PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_OBJ
            ]);
            $query = 'SELECT * FROM users where id = ?';
            $statment = $db->prepare($query);
            $statment->execute([$id]);


            foreach ($statment->fetchAll() as $row) {
                echo "<pre>";
                var_dump($row);
                // echo $row->email;
                echo "</pre>";
            }
        } catch (\PDOException $e) {
            echo $e->getMessage();
        }
```

### using named parameters

```php
$query = 'Insert into users (name, email) values (:name, :email)';
$statement = $db->prepare($query);
$statement->execute([
    ':name' => 'John Doe',
    ':email' => 'l7ZwH@example.com'
])
```

### Binding parameters by value and by reference

instead of using named parameters, we can bind parameters by value and by reference
```php
$email = 'l7ZwH@example.com';
$query = 'Insert into users (name, email) values (:name, :email)';
$statement = $db->prepare($query);
$statement->bindValue(':name', 'John Doe');
$statement->bindParam(':email', $email);

$statement->execute([]);
```

The difference between bindValue and bindParam is that the former binds by value, while the 
latter binds by reference.


### Note on PDO Emulated prepares
`PDO::ATTR_EMULATE_PREPARES` is a boolean flag that can be used to turn on/off 
emulated prepared statements.

Turning Emulated prepares usually will return the data from DB in its native format.
When Emulated prepares are turned on, the data will be returned as a string.
