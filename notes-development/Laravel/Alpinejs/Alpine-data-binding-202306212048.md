---
title: Alpine-data-binding
date: 21/06/2023
tags: alpinejs javascript laravel TALL-stack TALL
---

# **Alpine-data-binding** 202306212049 
> **785f58**

  

## Binding data
### x-data and x-text
Everything in alpinejs starts with the `x-data` directive.
```javascript
<div x-data="{ title: 'Start Here' }">
    <h1 x-text="title"></h1>
</div>
```
We pass a javascript object to the `x-data` directive then we can listen or bind to the data.
Here `x-text` will pass the string from `x-data` into the `h1` tag.


### x-html
`x-html` will pass the `innerHtml` attribute into the html tag:
```javascript
<div x-data="{ h1: '<h1>Title</h1>' }" x-html="h1">
</div>
```

### looping elements
In order to use looping in alpinejs we need to use a template tag and pass the loop:

```javascript
<div x-data="{ statuses: ['open', 'closed', 'archived'] }">
    <template x-for="status in statuses">
        <div x-text="status"></div>
    </template>
</div>
```


