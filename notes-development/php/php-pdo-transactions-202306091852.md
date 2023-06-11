---
title: php-pdo-transactions
date: 09/06/2023
tags: php pdo transaction db database dotenv
---

# **php-pdo-transactions** 202306091852 
> **c881ba**

  

## PHP transaction

In order to avoid situations where the input data is not always correct, we can use a transaction.
By wrapping our statements in within a transaction begin and a transaction commit, we can treat them as a single unit.

```php
try {
            $db->beginTransaction();

            $insert_user_statement = 'INSERT INTO users (email, full_name, is_active, created_at) VALUES (:email, :full_name, :is_active, :created_at)';

            $statment = $db->prepare($insert_user_statement);
            $statment->execute(['email' => $email, 'full_name' => $name, 'is_active' => $isactive, 'created_at' => $createdat]);

            $user_id = (int)$db->lastInsertId();

            $insert_invoice_statement = 'INSERT INTO invoices (amount, user_id) VALUES (:amount, :user_id)';
            $invoice_statement = $db->prepare($insert_invoice_statement);
            $invoice_statement->execute(['user_id' => $user_id, 'amount' => $amount]);

            $fetchStatement = $db->prepare('SELECT invoices.id AS invoice_id, amount, user_id, full_name FROM invoices
            INNER JOIN users ON invoices.user_id = users.id
            WHERE email = :email');
            $fetchStatement->execute(['email' => $email]);

            $db->commit();
        } catch (\PDOException $e) {
            echo $e->getMessage();
            if ($db->inTransaction()) {
                $db->rollBack();
            }
        }
```

It is important to catch exception in case something goes wrong in order to rollback the transaction.

## PHP Dotenv

Download the **dotenv** package through composer
`composer require vlucas/phpdotenv`

Load into php through:
```php
$dotenv = Dotenv\Dotenv::createImmutable(__DIR__);
$dotenv->load();
```
