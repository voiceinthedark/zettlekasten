---
title: Inertia-validation
date: 28/07/2023
tags: inertia vue laravel
---

# **Inertia-validation** 202307280237 
> **e9e18b**

  
## Form validation

Form validation in inertia is almost the same as in a typical Laravel application.

Here is a full form validation example.
We access the validation errors through the `errors` property: `$page.props.errors`.

We submit the form through Inertia `router`.
```javascript
// Inside our view
<template>

    <div class="mx-4">
        <span class="text-2xl">Create New User</span>
        <form action="/users/store" @submit.prevent="submit" method="post" class="mx-auto max-w-md border p-4 rounded">
            <div class="flex flex-col mt-6">
                <label for="name">Name</label>
                <input v-model="form.name" type="text" name="name" id="name" placeholder="Name" class="border p-2">
                <div v-if="$page.props.errors.name" class="text-red-500">{{ $page.props.errors.name }}</div>
            </div>
            <div class="flex flex-col mt-6">
                <label for="email">Email</label>
                <input v-model="form.email" type="email" name="email" id="email" class="border p-2" placeholder="Email">
                <div v-if="$page.props.errors.email" class="text-red-500">{{ $page.props.errors.email }}</div>
            </div>
            <div class="flex flex-col mt-6">
                <label for="password">Password</label>
                <input v-model="form.password" type="password" name="password" id="password" class="border p-2" placeholder="Password">
                <div v-if="$page.props.errors.password" class="text-red-500">{{ $page.props.errors.password }}</div>
            </div>
            <button type="submit" class="px-4 py-2 bg-emerald-600 text-white mt-2 rounded">Submit</button>
        </form>
    </div>



</template>

<script setup>
import { router } from '@inertiajs/vue3';
import { reactive } from 'vue';

const form = reactive({
    name: '',
    email: '',
    password: '',
})

function submit(){

    router.post('/users/store', form)
}
</script>

```

Then inside our controller we process validation as we normally
    do.

```php
Route::post('/users/store', function () {
   // validate the data
   Request::validate([
       'name' => 'required|max:15|min:5',
       'email' => 'required|email|unique:users',
       'password' => 'required',
   ]);
   // store the data
   User::create([
       'name' => Request::input('name'),
       'email' => Request::input('email'),
       'password' => bcrypt(Request::input('password')),
   ]);
   // redirect
   return redirect()->route('users.index');
});
```

