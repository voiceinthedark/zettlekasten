---
title: Laravel-socialite
date: 12/06/2023
tags: laravel github socialite oauth
---

# **Laravel-socialite** 202306121512 
> **009351**

  

## Adding Laravel Socialite

Download the laravel socialite package through composer
`composer require laravel/socialite`

Setup the configuration file inside services.php
```php
'github' => [
    'client_id' => env('GITHUB_CLIENT_ID'),
    'client_secret' => env('GITHUB_CLIENT_SECRET'),
    'redirect' => 'http://example.com/callback-url',
],
```

Assign the environment variables from github.
Then add the routes to web.php
```php
use Laravel\Socialite\Facades\Socialite;
 
Route::get('/auth/redirect', function () {
    return Socialite::driver('github')->redirect();
});
 
Route::get('/auth/callback', function () {
    $user = Socialite::driver('github')->user();
 
    // $user->token
});
```
