---
title: laravel-policy
date: 16/06/2023
tags: laravel php policy authorization
---

# **laravel-policy** 202306160422 
> **2fa145**

  

## Laravel Policies
Policies are needed in order to control what users can and cannot do.
To create a policy we use the `php artisan make:policy` command.
Inside the policy class we created we can then apply the policy to the user model.

```php

public function view(User $user, Post $post){
    return $user->id === $post->user_id;
}
```

Once our policy is set we need to enforce it in the api.php file.
```php
Route::middleware('auth:sanctum')->get('/posts/{post}', function (Post $post) {
    Gate::authorize('view', $post);

    return $post;
})
```

Policies can be registered in the AuthServiceProvider in the `$policies` property.

```php
/**
     * The policy mappings for the application.
     *
     * @var array
     */
    protected $policies = [
        Post::class => PostPolicy::class,
    ];
```


