---
title: php-file-system
date: 27/05/2023
tags: php file
---

# **php-file-system** 202305270029 
> **6a718f**

  

### File existence 
```php
if(!file_exists('foo.txt')) {
    echo 'File does not exist';
    return;
}

// ...
```

### Open File
```php
$file = fopen('foo.txt', 'r');
```

### read file
```php
while (($line = fgets($file)) !== false) {
    echo $line;
}
fclose($file);
```

### read CSV file
```php
while (($line = fgetcsv($file)) !== false) {
    print_r($line);
}
fclose($file);
```

### get entire file
```php
$content = file_get_contents('foo.txt');
```

### write into a file
```php
file_put_contents('foo.txt', 'Hello world');
```

#### append an existing file
```php
file_put_contents('foo.txt', 'Hello world', FILE_APPEND);
```

### delete a file
`unlink('foo.txt')`

### copy and move a file
```php
copy('foo.txt', 'bar.txt');
rename('foo.txt', 'bar.txt');
```
