---
title: Laravel-pagination
date: 19/06/2023
tags: laravel pagination
---

# **Laravel-pagination** 202306191558 
> **5f7324**

  

## Laravel Pagination

Pagination in laravel is easy to achieve; first instead of getting the posts you can use pagination to get the posts.
```php
$posts = Post::paginate(5);
```

After that inside our index view we can use the pagination like this:
```php
{{ $posts->links() }}
```
