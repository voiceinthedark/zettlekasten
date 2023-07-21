---
title: vue-directives-and-magic-methods
date: 19/07/2023
tags: vue sfc
---

# **vue-directives-and-magic-methods** 202307192302 
> **36c468**

  

## watchers

By using the `watch` method, you can observe changes in your data and react to them; we watch a property and wait for value change, if change occurs, we call a function or do whatever.

```javascript
<script>
export default {
  data() {
    return {
      todoId: 1,
      todoData: null
    }
  },
  methods: {
    async fetchData() {
      this.todoData = null
      const res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
      )
      this.todoData = await res.json()
    }
  },
  watch:{
    todoId(newVal){
      this.fetchData();
    },
  },
  mounted() {
    this.fetchData()
  }
}
</script>

<template>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</template>
```

## $refs or interacting with the DOM

```javascript
<script>
export default {
  mounted(){
    this.$refs.pElementRef.textContent = "Hiiii"
  },
}
</script>

<template>
  <p ref="pElementRef">hello</p>
</template>
```
