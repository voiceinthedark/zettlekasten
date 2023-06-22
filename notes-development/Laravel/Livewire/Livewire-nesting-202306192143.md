---
title: Livewire-nesting
date: 19/06/2023
tags: Livewire component events
---

# **Livewire-nesting** 202306192143 
> **de493f**

  

## Nesting livewire components
Livewire components can be nested inside each other.

```php
class HelloWorld extends Component
{
    // we can expose properties to the view by making them public
    public $contacts;

    public function mount(Contact $contact){
        $this->contacts = $contact::all();
    }

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
    @foreach ($contacts as $contact)
    @livewire('say-hi', ['name' => $contact->name], key($contact->id))
    @endforeach

</div>
```

Every child component is independent of the parent controller. They act as a single unit in order to 
minimize the payload.

## Events
A parent component can emit events to listeners:

```php
public function refreshChildren(){
    // emit event with parameter
    $this->emit('refresh', 'foo');
}
```

To capture the event, we listen to events on our child components:

```php
protected $listeners = ['refresh' => 'childrefresh'];

public function childrefresh($variable){
    // do something
    echo $variable;
}
```


