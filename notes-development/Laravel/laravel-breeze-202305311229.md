---
title: laravel-breeze
date: 31/05/2023
tags: php laravel breeze authentication
---

# **laravel-breeze** 202305311229 
> **6d585d**

  

## Laravel Breeze
Laravel Breeze is a minimal, simple implementation of all of Laravel's authentication features, including login, registration, password reset, email verification, and password confirmation.

### Installing Laravel breeze
```bash
composer require laravel/breeze --dev
 
php artisan breeze:install blade
# or
php artisan breeze:install vue
#or
php artisan breeze:install react
```

Once install, the frontend need to be refreshed:
`npm run dev`

And the database migrated:
`php artisan migrate`

