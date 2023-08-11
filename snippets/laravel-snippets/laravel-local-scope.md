# laravel-local-scope
#laravel #php #ORM #eloquent #eloquentORM #query

In order to maintain reusability, we can implement model scopes for queries that are used abundantly.

Here We want to fetch comments that have no parent comment, i.e root comments:
```php
// Defining a local scope to filter comments based on their parent
    public function scopeRootComments($query){
        return $query->whereNull('parent_id');
    }
```
A local scope method must begin with a `scope` keyword. It then can be called with a pascale case method name `rootComments`.

This can then be used in any query that needs to fetch root comments.

```php
$rootComment = Comment::rootComments()->first();
```
