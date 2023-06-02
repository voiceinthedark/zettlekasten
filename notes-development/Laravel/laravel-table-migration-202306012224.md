---
title: laravel-table-migration
date: 01/06/2023
tags: php laravel db database migration
---

# **laravel-table-migration** 202306012225 
> **329ed9**

  

## Migrate a database
```bash
php artisan migrate
```

In order to add fields to an already existing table:

```bash
php artisan make:migration name_of_migration_file --table=table_name
```

This will create a migration file:

## Migration file

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->addColumn('string', 'avatar')->after('email')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropColumn('avatar');
        });
    }
};

```
