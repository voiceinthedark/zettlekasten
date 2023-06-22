---
title: Laravel-relationships
date: 19/06/2023
tags: Laravel Database DB relationships
---

# **Laravel-relationships** 202306191619 
> **b262a7**

  

## Laravel relationships

### one-to-many
Inside our user model, we need to define a new method with a named `posts`:
```php
public function posts()
{
    return $this->hasMany(Post::class);
}
```

After that inside our Post model we need to define a new method with a named `user`:
```php
public function user()
{
    return $this->belongsTo(User::class);
}
```

Inside our blade templates we can access the relationship through the user variable
```php
@foreach($user->posts as $post)
{{ $post->title }} {{ $post->body }}
```

If we want to do the other way around we can do the following:
```php
@foreach($post->user as $user)
{{ $user->name }} 
@endforeach
``` 

### One to One relationship
A one to one relationship is easily created in Laravel.
First we need to define a new method in our Post model with a named `author`:
```php
public function author()
{
    return $this->belongsTo(User::class);
}
```

Then inside our User model we need to define a new method with a named `posts`:
```php
public function posts()
{
    return $this->hasOne(Post::class);
}
```

### Many to Many relationship
A many to many relationship is easily created in Laravel.
First we need to define a new method in our Post model with a named `categories`:
```php
public function categories()
{
    return $this->belongsToMany(Category::class);
}
```

Then inside our Comment model we need to define a new method with a named `post`:
```php
public function posts()
{
    return $this->belongsToMany(Post::class);
}
```
