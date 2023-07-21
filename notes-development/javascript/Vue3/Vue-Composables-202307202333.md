---
title: Vue-Composables
date: 20/07/2023
tags: vue composition-api
---

# **Vue-Composables** 202307202333 
> **aeb512**

  

## Composables

Composables are like traits in php. they encapsulate reusable code that can
be used in multiple components.

```javascript
/** useStorage.js */
import { ref, watch } from "vue";

export function useStorage(key, defaultValue = null) {
    const value = ref(localStorage.getItem(key) || defaultValue);
    
    if(!value.value) {
        localStorage.setItem(key, value.value)
    }

    watch(value, () => {
        localStorage.setItem(key, value.value)
    });    
    return value;
}
```

it can then be used in components:

```javascript
<script setup>
import { useFlash } from '@/components/composables/useFlash.js'
import { useStorage } from '@/components/composables/useStorage.js'

const flash = useFlash();
const food = useStorage('food', '');
const age = useStorage('age', '');


</script>

<template>
  <main>
    <button @click="flash.success('Click')">Click</button>
    <input type="text" name="food" id="food" v-model="food" />
    <input type="text" name="age" id="age" v-model="age" />
  </main>
</template>
```


