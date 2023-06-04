---
title: php-superglobals
date: 02/06/2023
tags: php globals routing
---

# **php-superglobals** 202306021832 
> **6a1629**

  

## Superglobals

### $_SERVER superglobal

Contains information about the server.

### implementing simple router using $_SERVER

```php
// Router.php
class Router {

    private array $routes = [];

    public function route(string $route, callable $action) : self {

        $this->routes[$route] = $action;        

        return $this;
    }

    public function resolve(string $request){


        $route = explode('?', $request)[0] ?? $request;
        $action = $this->routes[$route];

        if(!$action){
            throw new \InvalidArgumentException('404 error');
        }

        return call_user_func($action);

    }
}


// index.php

$route = new Router();

$route->route('/', function(){
    echo 'Home';
});

$route->route('/invoice', function(){
    echo 'Invoice';
});

$route->resolve($_SERVER['REQUEST_URI']);
```
