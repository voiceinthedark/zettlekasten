---
title: laravel-schemas
date: 04/06/2023
tags: laravel php schema database db
---

# **laravel-schemas** 202306042301 
> **886db8**

  

## Schema facade operations in laravel

### Adding foreign keys to a table
```php
Schema::table('table_name', function(Blueprint $table){
    $table->unsignedBigInteger('user_id');
    $table->foreign('user_id')->references('id')->on('table');

});


// Another method to add foreign keys to a table
// Laravel will automatically tries to search for the relevant foreign key
Schema::table('table_name', function(Blueprint $table){
    $table->foreignId('user_id')->constrained();
});

// In order to make the constraints explicit
Schema::table('table_name', function(Blueprint $table){
    $table->foreignId('user_id')->constrained(table: 'users');

});
```

### Creating a table through migration
```php
 public function up(): void
    {
        Schema::create('flights', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('airline');
            $table->timestamps();
        });
    }

    public function down() : void {
        Schema::drop('flights');
    }
```

### Updating table
In order to update a table 
```php
Schema::table('table_name', function(Blueprint $table){
    $table->unsignedBigInteger('user_id');
})
```

#### modifying columns
```php
Schema::table('table_name', function(Blueprint $table){
    $table->string('name', 50)->change();
})
```
