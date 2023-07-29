---
title: Inertia-shared-data
date: 27/07/2023
tags: inertia vue laravel
---

# **Inertia-shared-data** 202307271634 
> **06f602**

  

## Shared data

Inertia's server-side adapters all provide a method of making shared data available for every request. This is typically done outside of your controllers. Shared data will be automatically merged with the page props provided in your controller.
In Laravel applications, this is typically handled by the `HandleInertiaRequests` middleware.

```php
class HandleInertiaRequests extends Middleware
{
    public function share(Request $request)
    {
        return array_merge(parent::share($request), [
            // Synchronously...
            'appName' => config('app.name'),

            // Lazily...
            'auth.user' => fn () => $request->user()
                ? $request->user()->only('id', 'name', 'email')
                : null,
        ]);
    }
}
```

## Accessing shared data

```javascript
<script setup>
import { computed } from 'vue'
import { usePage } from '@inertiajs/vue3'

const page = usePage()

const user = computed(() => page.props.auth.user)
</script>

<template>
  <main>
    <header>
      You are logged in as: {{ user.name }}
    </header>
    <content>
      <slot />
    </content>
  </main>
</template>
```

### Sharing flash messages
```php
class HandleInertiaRequests extends Middleware
{
    public function share(Request $request)
    {
        return array_merge(parent::share($request), [
            'flash' => [
                'message' => fn () => $request->session()->get('message')
            ],
        ]);
    }
}
```

then we can access it using `$page.props.flash.message`:

```javascript
<template>
  <main>
    <header></header>
    <content>
      <div v-if="$page.props.flash.message" class="alert">
        {{ $page.props.flash.message }}
      </div>
      <slot />
    </content>
    <footer></footer>
  </main>
</template>
```
