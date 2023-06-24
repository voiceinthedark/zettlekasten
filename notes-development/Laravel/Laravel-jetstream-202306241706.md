---
title: Laravel-jetstream
date: 24/06/2023
tags: laravel jetstream authentication
---

# **Laravel-jetstream** 202306241707 
> **bfdb78**

  
# Laravel Jetstream

## Banner Alerts
To send banner alerts to the top of the screen we can pass them through sessions:

```php
$request->session()->flash('flash.banner', 'Yay it works!');
$request->session()->flash('flash.bannerStyle', 'success');

return redirect('/');
```

Or through redirect responses:

```php
return redirect()->route('subscriptions')->banner('Subscription created successfully.');

return redirect()->route('subscriptions')->dangerBanner('Subscription cancellation failed.');
```

## Customizing password validation rules
To customize password validation rules `App\Actions\Fortify\PasswordValidationRules` trait utilizes a custom `Laravel\Fortify\Rules\Password`.

```php
use Laravel\Fortify\Rules\Password;

// Require at least 10 characters...
(new Password)->length(10)

// Require at least one uppercase character...
(new Password)->requireUppercase()

// Require at least one numeric character...
(new Password)->requireNumeric()

// Require at least one special character...
(new Password)->requireSpecialCharacter()
```

## Modal Password Confirmation

The following documentation will discuss how to use modal based password confirmation in Jetstream. Modal based password authentication is typically used when you would like the user to confirm their password before performing a specific action, such as when enabling two-factor authentication.

This form of password confirmation displays a modal window that allows the user to confirm their password before their intended request is executed.

![Screenshot of Password Confirmation](https://jetstream.laravel.com/assets/img/modal-confirm.29bb2150.png)

### [#](https://jetstream.laravel.com/3.x/features/password-update.html#modal-password-confirmation-via-livewire) Modal Password Confirmation Via Livewire

#### [#](https://jetstream.laravel.com/3.x/features/password-update.html#component-preparation) Component Preparation

If you are using the Livewire stack, the Livewire component that contains the action that should require password confirmation before being invoked should use the `Laravel\Jetstream\ConfirmsPasswords` trait.

#### [#](https://jetstream.laravel.com/3.x/features/password-update.html#the-confirms-password-blade-component) The `confirms-password` Blade Component

Next, in your application's user interface, you should wrap the button that triggers the action within the `confirms-password` Blade component. The `confirms-password` wrapper component should contain a `wire:then` directive that specifies which Livewire action should be run once the user's password has been confirmed:

```html
<x-confirms-password wire:then="enableAdminMode">
    <x-button type="button" wire:loading.attr="disabled">
        {{ __('Enable') }}
    </x-button>
</x-confirms-password>
```

#### [#](https://jetstream.laravel.com/3.x/features/password-update.html#ensuring-the-password-is-confirmed) Ensuring The Password Is Confirmed

After adding the `confirms-password` component to your application's user interface, you should call the `ensurePasswordIsConfirmed` method within the Livewire action that requires password confirmation. This should be done at the very beginning of the relevant action method:

```php
/**
 * Enable administration mode for user.
 */
public function enableAdminMode(): void
{
    $this->ensurePasswordIsConfirmed();

    // ...
}
```

