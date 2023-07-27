---
title: Inertia-Pagination
date: 27/07/2023
tags: inertia pagination vue
---

# **Inertia-Pagination** 202307271835 
> **a2acf3**

  

### Inertia-Pagination
Paginating through data in inertia requires a few things. 

First in the controller we need to map through the data.

```php
Route::get('/', function () {
    return inertia('Welcome', [
        'users' => User::paginate(10)->through(function ($user) {
            return [
                'id' => $user->id,
                'name' => $user->name,
                'email' => $user->email,
            ];
        }),
    ]);
});
```

Then we can paginate through the data on the client side as a *pagination object*:

```vue
<script setup>
import { Link } from "@inertiajs/vue3";
defineProps({
    name: String,
    users: Object,
});
</script>
 <!-- Paginate -->
        <div>
            <ul class="flex flex-row gap-1">
                <li v-for="link in users.links" :key="link.label">
                    <Link
                        :href="link.url"
                        v-html="link.label"
                        :class="link.active ? 'bg-emerald-300' : ''"
                    />
                </li>
            </ul>
        </div>
    </div>
```
