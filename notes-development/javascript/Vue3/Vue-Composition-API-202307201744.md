---
title: Vue-Composition-API
date: 20/07/2023
tags: vue composition-api
---

# **Vue-Composition-API** 202307201744 
> **491733**

  

## Reactivity, ref and reactive

```javascript
<script setup>
import { ref } from 'vue'

// component logic
// declare some reactive state here.
  const message = ref('A Test');
</script>

<template>
  <h1 v-text="message"></h1>
</template>
```

reactive() only works on objects (including arrays and built-in types like Map and Set). ref(), on the other hand, can take any value type and create an object that exposes the inner value under a .value property:

```javascript
import { reactive } from 'vue'

const counter = reactive({
  count: 0
})

console.log(counter.count) // 0
counter.count++
```

Reactive data using `ref` can only be accessed through the `value` property:
```javascript
<script setup>
import { ref } from 'vue'

let count = ref(0)
function increment(){
  count.value++;
}
</script>

<template>
  <!-- make this button work -->
  <button @click="increment">count is: {{ count }}</button>
</template>
```

### more examples

```javascript
<script setup>
import { ref } from 'vue'

// give each todo a unique id
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
  { id: id++, text: 'Learn Vue' }
])

function addTodo() {
  todos.value.push({id: id++, text: newTodo.value});
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter(t => t != todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
```

### Computed properties

```javascript
<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter(t => t.done == false) : todos.value;
});
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```

## refs and lifecycle hooks

The difference between Options Api and Composition Api is that in Options Api
    we access the refs through the `$refs` magic method:
    `this.$refs.elementname`. While in Composition api we only need to use `ref`:
    `const pElementRef = ref(null)`

```javascript
<script setup>
import { ref, onMounted } from 'vue'

const pElementRef = ref(null)

onMounted(() => {
  pElementRef.value.textContent = "Hi"
});
</script>

<template>
  <p ref="pElementRef">hello</p>
</template>
```

## Watcher

```javascript
<script setup>
import { ref, watch } from 'vue'

const todoId = ref(1)
const todoData = ref(null)

async function fetchData() {
  todoData.value = null
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  todoData.value = await res.json()
}

  watch(todoId, (newId) => {
    fetchData()
  })
  
fetchData()
</script>

<template>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++">Fetch next todo</button>
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</template>
```

## Props

```javascript
/** child component */
<script setup>
const props = defineProps({
  msg: String
})
</script>

<template>
  <h2>{{ msg || 'No props passed yet' }}</h2>
</template>
```

```javascript
/** Parent */
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const greeting = ref('Hello from parent')
</script>

<template>
  <ChildComp :msg="greeting" />
</template>
```

## Emiting events

```javascript
/** Child */
<script setup>
const emit = defineEmits(['response'])

emit('response', 'hello from child')
</script>

<template>
  <h2>Child component</h2>
</template>
```

```javascript
/** Parent */
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const childMsg = ref('No child msg yet')
</script>

<template>
  <ChildComp @response="(msg) => childMsg = msg" />
  <p>{{ childMsg }}</p>
</template>
```

