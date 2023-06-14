---
title: Laravel-sail-permissions
date: 13/06/2023
tags: laravel sail php permissions docker
---

# **Laravel-sail-permissions** 202306130128 
> **22de8d**

  
### Permission denied with docker and sail[1]

Solving this problem require setting the WWWWUSER in the app environment to be equal to the main user id.
Basically on my OS it is **1000**

To check user id on linux: `id -u` 
To check for user group id: `id -g`

### Not Working?
Resort to chmod the entire folder to othere read/write
`chmod -R o+rw /path/to/folder`

[1]: <https://github.com/laravel/sail/issues/81>