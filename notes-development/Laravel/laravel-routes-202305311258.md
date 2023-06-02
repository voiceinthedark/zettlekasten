---
title: laravel-routes
date: 31/05/2023
tags: laravel php routing
---

# **laravel-routes** 202305311258 
> **8ace12**

  

## Creating a route for the controller
Routes are stored in the `routes` directory of the project.
Inside web.php:
```PHP
use App\Http\Controller\ChirpController;
// ...
Route::resource('chirps', ChirpController::class) # call a resource route
    ->only(['index', 'store']) # use it on main page and save page
    ->middleware(['auth', 'verified']); # only Authorized and verified users
```

this will create the following routes:

| Verb |   URI   | Action |   Route Name |
| :--- | :-----: | :----: | -----------: |
| GET  | /chirps | index  | chirps.index |
| POST | /chirps | store  | chirps.store |

