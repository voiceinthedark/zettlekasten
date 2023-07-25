---
title: Vue-stores-state-management
date: 21/07/2023
tags: vue composition-api state state-management
---

# **Vue-stores-state-management** 202307211927 
> **d2aadf**

  

## External stores

A simple store accessible across the entire application

```javascript
/** Inside stores/counterStore.js */
<script setup>
import { counter } from '@/stores/counterStore.js';

</script>

<template>
    <div id="counter" class="counter">
        <h1>Counter</h1>
        <span>{{ counter.count }}</span>
        <button @click="counter.increment()">Increase</button>
    </div>
</template>

<style scoped>
.counter{
    display: flex;
    flex-direction: column;
    gap: 2rem;
}
span{
    font-size: 16em;
}
</style>
```

And we can access it from anywhere in the app by importing the state.

## Pinia for state management

`npm install pinia`

```javascript
import { defineStore } from "pinia";

export const useCounterStore = defineStore("counter", {
    state: () => ({
        count: 0,
    }),
    actions: {
        increment() {
            this.count++;
        }
    },
    getters: {
        doubleCount: (state) => {
            return state.count * 2
        }
    }
})
```
