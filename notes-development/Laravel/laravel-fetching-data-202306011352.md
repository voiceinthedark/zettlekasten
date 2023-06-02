---
title: laravel-fetching-data
date: 01/06/2023
tags: php DB laravel database
---

# **laravel-fetching-data** 202306011352 
> **1ba4ce**

  
## Running SQL Queries
Once you have configured your database connection, you may run queries using the DB facade. The DB facade provides methods for each type of query: select, update, insert, delete, and statement.

```php
$users = DB::select('select * from users');
    dd($users);
```

### Searching by bindings
```PHP
$users = DB::select('select * from users where email=?', ['abc@email.com']);
    dd($users);
```

## Laravel Query builder

### Get data
```php
$users = DB::table('users')->get();
// ...
$user = DB::table('users')->where('name', 'John')->first(); 
return $user->email;
// To retrieve a single row by its id column value, use the find method:
$user = DB::table('users')->find(3);
// retrieve a column value
$email = DB::table('users')->where('name', 'John')->value('email');
```

### insert data

```php
DB::table('users')->insert([
    'email' => 'kayla@example.com',
    'votes' => 0
]);
```

### update data
```php
$affected = DB::table('users')
              ->where('id', 1)
              ->update(['votes' => 1]);
```

### delete data
```php
$deleted = DB::table('users')->delete();
 
$deleted = DB::table('users')->where('votes', '>', 100)->delete();
```

## Eloquent (ORM)
When using Eloquent, each database table has a corresponding "Model" that is used to interact with that table. In addition to retrieving records from the database table, Eloquent models allow you to insert, update, and delete records from the table as well.

### Generating a model
`php artisan make:model Flight`

#### Generating a model with migration and controller
`php artisan make:model Flight -mc`

### Fetching data by model
```php
use App\Models\Flight;
 
// Retrieve a model by its primary key...
$flight = Flight::find(1);
 
// Retrieve the first model matching the query constraints...
$flight = Flight::where('active', 1)->first();
 
// Alternative to retrieving the first model matching the query constraints...
$flight = Flight::firstWhere('active', 1);

// ...
$flight = Flight::findOr(1, function () {
    // ...
});
 
$flight = Flight::where('legs', '>', 3)->firstOr(function () {
    // ...
});

// ...
use App\Models\Flight;
 
// Retrieve flight by name or create it if it doesn't exist...
$flight = Flight::firstOrCreate([
    'name' => 'London to Paris'
]);
 
// Retrieve flight by name or create it with the name, delayed, and arrival_time attributes...
$flight = Flight::firstOrCreate(
    ['name' => 'London to Paris'],
    ['delayed' => 1, 'arrival_time' => '11:30']
);
 
// Retrieve flight by name or instantiate a new Flight instance...
$flight = Flight::firstOrNew([
    'name' => 'London to Paris'
]);
 
// Retrieve flight by name or instantiate with the name, delayed, and arrival_time attributes...
$flight = Flight::firstOrNew(
    ['name' => 'Tokyo to Sydney'],
    ['delayed' => 1, 'arrival_time' => '11:30']
);

// Retrieving aggregates

$count = Flight::where('active', 1)->count();
 
$max = Flight::where('active', 1)->max('price');
```

### Inserting and updating models

```php
<?php
 
namespace App\Http\Controllers;
 
use App\Http\Controllers\Controller;
use App\Models\Flight;
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
 
class FlightController extends Controller
{
    /**
     * Store a new flight in the database.
     */
    public function store(Request $request): RedirectResponse
    {
        // Validate the request...
 
        $flight = new Flight;
 
        $flight->name = $request->name;
 
        $flight->save();
 
        return redirect('/flights');
    }
}
```

we assign the name field from the incoming HTTP request to the name attribute of the App\Models\Flight model instance. When we call the save method, a record will be inserted into the database

Alternatively, you may use the create method to "save" a new model using a single PHP statement. The inserted model instance will be returned to you by the create method:

```php
use App\Models\Flight;
 
$flight = Flight::create([
    'name' => 'London to Paris',
]);
```

name field must be fillable in order to use create method. In order to protect from malicious code,
Laravel turns mass assignment off.

To turn mass assignment on certain model fields:

```php
<?php
 
namespace App\Models;
 
use Illuminate\Database\Eloquent\Model;
 
class Flight extends Model
{
    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = ['name'];
}
```
#### Updating records
```php
use App\Models\Flight;
 
$flight = Flight::find(1);
 
$flight->name = 'Paris to London';
 
$flight->save();
```

##### Mass updating
```php
Flight::where('active', 1)
      ->where('destination', 'San Diego')
      ->update(['delayed' => 1]);
```

### Examining attribute changes

- isDirty() and isClean()
  ```php
  use App\Models\User;
   
  $user = User::create([
      'first_name' => 'Taylor',
      'last_name' => 'Otwell',
      'title' => 'Developer',
  ]);
   
  $user->title = 'Painter';
   
  $user->isDirty(); // true
  $user->isDirty('title'); // true
  $user->isDirty('first_name'); // false
  $user->isDirty(['first_name', 'title']); // true
   
  $user->isClean(); // false
  $user->isClean('title'); // false
  $user->isClean('first_name'); // true
  $user->isClean(['first_name', 'title']); // false
   
  $user->save();
   
  $user->isDirty(); // false
  $user->isClean(); // true
  ```
- wasChanged()
  ```php
    $user = User::create([
      'first_name' => 'Taylor',
      'last_name' => 'Otwell',
      'title' => 'Developer',
  ]);
   
  $user->title = 'Painter';
   
  $user->save();
   
  $user->wasChanged(); // true
  $user->wasChanged('title'); // true
  $user->wasChanged(['title', 'slug']); // true
  $user->wasChanged('first_name'); // false
  $user->wasChanged(['first_name', 'title']); // true

  ```
- getOriginal()
  ```php
  $user = User::find(1);
 
  $user->name; // John
  $user->email; // john@example.com
   
  $user->name = "Jack";
  $user->name; // Jack
   
  $user->getOriginal('name'); // John
  $user->getOriginal(); // Array of original attributes...
  ```

## Deleting models

```php
use App\Models\Flight;
 
$flight = Flight::find(1);
 
$flight->delete();
```

You may call the truncate method to delete all of the model's associated database records. The truncate operation will also reset any auto-incrementing IDs on the model's associated table:

```php
Flight::truncate();
```

### Deleting by primary key
```php
Flight::destroy(1);
 
Flight::destroy(1, 2, 3);
 
Flight::destroy([1, 2, 3]);
 
Flight::destroy(collect([1, 2, 3]));
```

The destroy method loads each model individually and calls the delete method so that the deleting and deleted events are properly dispatched for each model.

### Delete using queries
```php
$deleted = Flight::where('active', 0)->delete();
```

## Soft Deletes
In addition to actually removing records from your database, Eloquent can also "soft delete" models. When models are soft deleted, they are not actually removed from your database. Instead, a deleted_at attribute is set on the model indicating the date and time at which the model was "deleted". To enable soft deletes for a model, add the Illuminate\Database\Eloquent\SoftDeletes trait to the model:

```php
<?php
 
namespace App\Models;
 
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;
 
class Flight extends Model
{
    use SoftDeletes;
}
```

Adding `deleted_at` column to database table:
```php
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
 
Schema::table('flights', function (Blueprint $table) {
    $table->softDeletes();
});
 
Schema::table('flights', function (Blueprint $table) {
    $table->dropSoftDeletes();
});
```

### Restoring soft deleted models
To restore a soft deleted model, you may call the restore method on a model instance. The restore method will set the model's deleted_at column to null:
```php
$flight->restore();
```

### Querying soft deleted models
```php
use App\Models\Flight;
 
$flights = Flight::withTrashed()
                ->where('account_id', 1)
                ->get();
```
### Retrieving only soft deleted models
```php
$flights = Flight::onlyTrashed()
                ->where('airline_id', 1)
                ->get();
```


