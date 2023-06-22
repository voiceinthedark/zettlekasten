---
title: Livewire-data-binding
date: 16/06/2023
tags: Livewire php blade laravel data-static-binding
---

# **Livewire-data-binding** 202306162222 
> **ea747d**

  

## Livewire Data Binding

By creating a livewire component `php artisan make:livewire component_name` we get two files generated:
The view.blade file template and the livewire component class.

To data bind we need to pass the data from the component class (A controller) to the blade view:

```php
class HelloWorld extends Component
{
    public function render()
    {
        return view('livewire.hello-world', [
            'name' => 'John Doe',
        ]);
    }
}

```

We can bind the data in our template as usual
```php
<h1>Hello {{ $name }}</h1>
```

### Binding in our wire view

To bind the data in our wire view we use the `wire:model` attribute:
```php
<div>
    <input type="text" wire:model="name">
    Hello {{ $name}}
</div>
```

To debounce the input we can use the `wire:debounce` attribute:
```php
<div>
    <input type="text" wire:model.debounce.500ms="name">
    Hello {{ $name}}
</div>
```
This will make our request wait for 500ms before being sent out.
Or we can use the lazy binding:
```php
<div>
    <input type="text" wire:model.lazy="name">
    Hello {{ $name}}
</div>
```
This will only send a request only once the input loses focus.

### More databinding options

```php
class HelloWorld extends Component
{
    // we can expose properties to the view by making them public
    public string $name = 'John Doe';
    public bool $loud = false;
    public array $greeting = ["hello"];
    public function render()
    {
        return view('livewire.hello-world', [
            // Or we can pass them as data to the view
            // 'name' => 'John Doe',
        ]);
    }
}

---

<div>
    <input type="text" wire:model="name">
    <input type="checkbox" name="loud" id="loud" wire:model="loud">
    <select name="greeting" id="greeting" wire:model="greeting" multiple>
        <option value="hello">Hello</option>
        <option value="hi">Hi</option>
        <option value="goodbye">Goodbye</option>
    </select>


    {{ Arr::join($greeting, ', ') }} {{ $name}} @if ($loud) ! @endif

</div>
```


