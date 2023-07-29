---
title: Inertia-form-helper
date: 28/07/2023
tags: inertia vue forms laravel
---

# **Inertia-form-helper** 202307280347 
> **03decd**

  

## Inertia form helper

To use the form helper we need to import `useForm` composable.
and instead of using the `router` method we use the form.

```javascript
<script setup>
import { router, useForm } from '@inertiajs/vue3';
import { reactive } from 'vue';

const form = useForm({
    name: '',
    email: '',
    password: '',
})

function submit(){

    form.post('/users/store');
}
</script>
```

### form helper progressbar
We can use the progress attribute to show progress when uploading.


