---
title: Laravel-authetication
date: 22/06/2023
tags: laravel authentication
---

# **Laravel-authetication** 202306222209 
> **667757**

  

## Session based authentication
A session based authentication is a way of storing the user's authentication details in a session. This is done by creating a session with the user's email and password. Once the user is authenticated, the session is saved and the user is redirected to the dashboard.

To manually authenticate users we create an Authcontroller; inside the login function we need to validate the authentication details.

```php
public function login(){
    validator::make(request()->all(), [
        'email' => 'required|email',
        'password' => 'required'
    ])->validate();

    // if the details are validated redirect to the dashboard
    if( auth()->attempt(request()->only('email', 'password'))){
        return redirect()->route('dashboard');
    }
    return back()->withErrors(['email' => 'Invalid Credentials']);
}
```

### Logout the user
```php
public function logout(){
    // now the session will be invalidated
    auth()->logout();
}
```

It is important to wrap our dashboard as well as any need-to-autheticate route in a authenticate middleware.
by simply appending the route with `middlware('auth')`.

### Adding a remember me
we can extract a remember me by extracting and autheticating the remember me checkbox during login.
```php
public function login(){
    validator::make(request()->all(), [
        'email' => 'required|email',
        'password' => 'required'
    ])->validate();

    // if the details are validated redirect to the dashboard
    if( auth()->attempt(    
        request()->only('email', 'password'), 
        $request->filled('remember'))){ // checking if the remember me is checked
        return redirect()->route('dashboard');
    }
    return back()->withErrors(['email' => 'Invalid Credentials']);
}

```

## Token Based authetication



