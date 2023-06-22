---
title: Livewire-Actions
date: 19/06/2023
tags: Livewire javascript laravel
---

# **Livewire-Actions** 202306191917 
> **8da3c8**

  

### Livewire Actions
To listen to actions in livewire components we use the `wire:action` attribute.

```php
<button wire:click="resetName($event.target.innerText)">Reset Name</button>
---
public function resetName($name)
    {
        $this->name = $name;
    }
```

The `$event` is a magic method that capture the same function as the event in javascript.

#### Many actions types
Actions can be many types:
```
wire.click
wire.mouseenter
wire.mouseover
wire.custom-event
```

When dealing with forms we need the `wire.submit` attribute.
```php
<form action="#" wire:submit.prevent="resetName('john')">
        <button>Reset Name</button>
    </form>
```

we use `wire.submit.prevent` so that the form does not submit. same as `e.preventDefault()` in javascript.


