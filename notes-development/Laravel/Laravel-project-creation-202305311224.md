---
title: Laravel-project-creation
date: 31/05/2023
tags: php laravel bash composer docker-composer
---

# **Laravel-project-creation** 202305311224 
> **089b8f**

  

## Creating a laravel project
`composer create-project laravel/laravel chirper`

Run the server:
`php artisan serve`

### Creating a laravel project through docker
```bash
curl -s "https://laravel.build/chirper" | bash
cd prject-directory
./vendor/bin sail up
```

## Using bash commands through Laravel sail
```bash
./vendor/bin/sail php --version
./vendor/bin/sail artisan --version
./vendor/bin/sail composer --version
./vendor/bin/sail npm --version
```


