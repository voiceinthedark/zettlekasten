---
title: laravel-events-listeners
date: 22/06/2023
tags: Laravel events listeners
---

# **laravel-events-listeners** 202306220225 
> **0d18e9**

  

## Events and listeners
`php artisan event:generate` will generate the events and listeners that are registered in the 
EventServiceProvider.

Alternatively, you may use the make:event and make:listener Artisan commands to generate individual events and listeners:
```bash
php artisan make:event MyEvent
php artisan make:listener MyListener --event=MyEvent
```

### Registering the events
Typically Events are passed to the array $listen of the EventServiceProvider:
```php
protected $listen = [
    OrderShipped::class => [
        SendShipmentNotification::class,
    ],
];
```

## Defining Events
An event class is essentially a data container which holds the information related to the event.

```php
<?php
 
namespace App\Events;
 
use App\Models\Order;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Foundation\Events\Dispatchable;
use Illuminate\Queue\SerializesModels;
 
class OrderShipped
{
    use Dispatchable, InteractsWithSockets, SerializesModels;
 
    /**
     * Create a new event instance.
     */
    public function __construct(
        public Order $order,
    ) {}
}
```

## Defining listeners

```php
<?php
 
namespace App\Listeners;
 
use App\Events\OrderShipped;
 
class SendShipmentNotification
{
    /**
     * Create the event listener.
     */
    public function __construct()
    {
        // ...
    }
 
    /**
     * Handle the event.
     */
    public function handle(OrderShipped $event): void
    {
        // Access the order using $event->order...
    }
}
```

## Queued Events
If our events need to take time to process and to run asynchronously. We need to send the event to a Queue.
This is simple in Laravel; the event need to implement the ShouldQueue interface.

## Dispatching events
To dispatch events we need to manually call the `dispatch` method.
```php
<?php
 
namespace App\Http\Controllers;
 
use App\Events\OrderShipped;
use App\Http\Controllers\Controller;
use App\Models\Order;
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
 
class OrderShipmentController extends Controller
{
    /**
     * Ship the given order.
     */
    public function store(Request $request): RedirectResponse
    {
        $order = Order::findOrFail($request->order_id);
 
        // Order shipment logic...
 
        OrderShipped::dispatch($order);
 
        return redirect('/orders');
    }
}
```

## Elequent ORM events
Elequent ORM can dispatches many events, so we need to use the `dispatchesEvent` method.
```php
<?php
 
namespace App\Models;
 
use App\Events\UserDeleted;
use App\Events\UserSaved;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
 
class User extends Authenticatable
{
    use Notifiable;
 
    /**
     * The event map for the model.
     *
     * @var array
     */
    protected $dispatchesEvents = [
        'saved' => UserSaved::class,
        'deleted' => UserDeleted::class,
    ];
}
```

## Observer
If you are listening for many events on a given model, you may use observers to group all of your listeners into a single class. Observer classes have method names which reflect the Eloquent events you wish to listen for. Each of these methods receives the affected model as their only argument. The make:observer Artisan command is the easiest way to create a new observer class:

`php artisan make:observer MyObserver --model=User`

To register an observer, you need to call the observe method on the model you wish to observe. You may register observers in the boot method of your application's App\Providers\EventServiceProvider service provider:
```php
use App\Models\User;
use App\Observers\UserObserver;
 
/**
 * Register any events for your application.
 */
public function boot(): void
{
    User::observe(UserObserver::class);
}
```

Or:

```php
use App\Models\User;
use App\Observers\UserObserver;
 
/**
 * The model observers for your application.
 *
 * @var array
 */
protected $observers = [
    User::class => [UserObserver::class],
];
```



