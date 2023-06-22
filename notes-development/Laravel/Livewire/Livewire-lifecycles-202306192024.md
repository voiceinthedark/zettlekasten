---
title: Livewire-lifecycles
date: 19/06/2023
tags: Livewire laravel lifecycle
---

# **Livewire-lifecycles** 202306192024 
> **9d071e**

  

## Livewire lifecycles

### Mount lifecycle
The mount lifecycle is triggered when the component is mounted. It is triggered after the component has been created.

```php
// we can also expose methods to the view by making them public
    // Livewire exposes the mount() method which runs when the component is mounted on the DOM and only for one time
    // the mount method can accept arguments, including the Request object
    // Other methods cannot accept the Request object
    public function mount(Request $request, string $name){
        $this->name = $request->input('name', $name);
    }
```

### Updated lifecycle
The updated lifecycle is triggered when the component is updated.
```php
public function updated($name){
    // emit in this case will trigger the `updated` event
    $this->emit('updated', $name);
}
```

The updated lifecycle method can also be dynamically adapted to properties
For example if we have a public name property we can call `updatedName` lifecycle method that is triggered when the name gets updated.
