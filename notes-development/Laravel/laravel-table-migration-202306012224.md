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

## Database seeders
Seeders will populate the database with data:
`php artisan make:seeder name_of_seeder`

inside the run method of our seeder:
```php
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

public funtion run(){
    $posts = [
        [
            'title' => 'Post 1',
            'excerpt' => 'post 1 summary'
            'body' => 'Post 1 body'
            'min_to_read' => 2,
        ],
        [
            'title' => 'Post 2',
            'excerpt' => 'post 2 summary'
            'body' => 'Post 2 body'
            'min_to_read' => 2,
        ],
    ];

    foreach ($posts as $key => $value) {
        Post::create($value);
    }
}
```

Then inside the DatabaseSeeder class's run method we invoke our PostSeeder class:
```php
public function run(){
    $this->call([
        PostSeeder::class,
    ])
}
```

### Running the migration with a seed
`php artisan migrate:reset` To reset the tables
`php artisan migrate --seed`

If the tables are already migrated:
`php artisan db:seed`

## Artisan DB Commands
To rollback and reinstate a database
`php artisan migrate:refresh`

To rollback a database
`php artisan migrate:reset`

To show database information:
`php artisan db:show`

To show table information:
`php artisan db:table table_name`

## Database Factories
Factories inject fake data into the database.

To create a factory class run the artisan command:
`php artisan make:factory factory_name`

Inside our factory class definition method:
```php
return [
    'title' => $this->faker->unique()->sentence(),
    'excerpt' => $this->faker->realText($maxNbChars=50),
    'body' => $this->faker->text(),
    'image_path' => $this->faker->imageUrl(64,64),
    'is_published' => 1,
    'min_to_read' => $this->faker->numberBetween(1, 10),
];
```

Then inside the DatabaseSeeder class, run method:

```php
// This will create 10 fake posts and save them to the database
Post::factory(10)->create();
```

In the end we need to run the seed command from the cli:
`php artisan db:seed`

