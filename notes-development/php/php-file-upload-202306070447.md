---
title: php-file-upload
date: 07/06/2023
tags: php file-upload
---

# **php-file-upload** 202306070447 
> **8342ae**

  
## File upload
in order to enable file uploading the enctype of the form must be set to `multipart/form-data`.

```php
public function index(): string
    {
        $title = '<h1>Home Page</h1>';
        $form = <<<HTML
        <form action="/upload" method="post" enctype="multipart/form-data">
            Upload File: <input type="file" name="file">
            <input type="submit" value="Upload">
        </form>
    HTML;

        return $title . $form;
    }
```

In the above example our Home.php class accepts get request on the index() method. relaying to the root '/'.

Accepting the request through our router class:
```php

public function get(string $route, callable|array $action): self
    {
        return $this->route('get', $route, $action);
    }


public function resolve(string $request, string $request_method = 'get')
    {


        $route = explode('?', $request)[0] ?? $request;
        $action = $this->routes[$request_method][$route];

        if (!$action) {
            throw new \InvalidArgumentException('404 error');
        }

        if (is_callable($action)) {
            call_user_func($action);
        }

        if (is_array($action)) {
            [$class, $method] = $action;
            if (class_exists($class)) {
                $instance = new $class();
                if (method_exists($instance, $method)) {
                    $reflection_return = new ReflectionMethod($instance, $method);
                    if ($reflection_return->getReturnType()->getName() === 'void') {
                        $instance->$method();
                    } else {
                        echo $instance->$method();
                    }
                }
            }
        }
    }
```

finally we capture the file upload on the index page:

```php
$route->get('/', [Home::class, 'index'])
      ->get('/invoice', [Invoice::class, 'index'])
      ->get('/invoice/create', [Invoice::class, 'create'])
      ->post('/invoice/create', [Invoice::class, 'store'])
      ->post('/upload', [Home::class, 'upload']);
```

The form relays the action to the '/upload' path, which is mapped to our upload() function on the Home class.

```php
// we're just printing the value of the $_FILES superglobal
public function upload() : void
    {
        echo "<pre>";
        var_dump($_FILES['file']);
        echo "</pre>";
    }
```

## File uploading procedure
The file is usually uploaded to a temporary folder on the server.
In order to get the file to the server we need to use the `move_uploaded_file()` function.

```php
// Here STORAGE_PATH is a constant that holds the path to the server storage
move_uploaded_file($_FILES['file']['tmp_name'], STORAGE_PATH . '/' . $_FILES['file']['name']);
```

### Important note when working on docker
When working with a docker container, File upload might not work due to permission access.
In order to fix this problem, on the shell run the command to access the container bash:
`docker exec -it <php_laravel-app> /bin/bash`

After entering the shell terminal, give access rights to the user, usually `www-data` on nginx.
```bash
root@47db2d576b29:/var/www# chown -R www-data:www-data /var/www/
root@47db2d576b29:/var/www# find /var/www/ -type d -exec chmod 775 {} \;
```
### Accepting multiple files upload
By giving the form input name an array designation, the form will then accept multiple file uploads

```php
<form action="/upload" method="post" enctype="multipart/form-data">
    Upload File: <input type="file" name="file[]" multiple>
    <input type="submit" value="Upload">
</form>
```
