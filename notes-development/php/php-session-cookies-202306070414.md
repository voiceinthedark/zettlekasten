---
title: php-session-cookies
date: 07/06/2023
tags: php session cookies   
---

# **php-session-cookies** 202306070415 
> **4337f1**


## php Sessions

To start a session, you can use the `session_start()` function.

Sessions can be set and unset:
```php
$_SESSION['foo'] = 'bar';
unset($_SESSION['foo']);
```

## php Cookies
Cookies can be set and unset:
```php
setcookie('username', 'firas', time() + 3600);
// To unset a cookie use a negative value for expiration
setcookie('username', '', time() - 3600);

// To access a cookie, use the $_COOKIE superglobal
echo $_COOKIE['username'];
```
  

