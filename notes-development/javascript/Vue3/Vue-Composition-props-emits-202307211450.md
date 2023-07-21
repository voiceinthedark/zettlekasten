---
title: Vue-Composition-props-emits
date: 21/07/2023
tags: vue composition-api sfc
---

# **Vue-Composition-props-emits** 202307211450 
> **6207cb**

  

## Props and events

```javascript
/** Home */
<script setup>
import { ref } from 'vue';
import TabbableTextarea from '../components/TabbableTextarea.vue';

const tareaValue = ref('Hello World');

</script>

<template>
  <main>
    <TabbableTextarea v-model="tareaValue" style="height: 300px; width: 300px" />
  </main>
</template>

```

We define props in the chld component through defineProps macro and events 
through defineEmits macro.

```javascript
<script setup>

defineProps({
    modelValue: String
});

let emit = defineEmits(['update:modelValue']);

function onTabPress(e){
    // Add tab whenever tab is pressed
    let textarea = e.target;
    let start = textarea.selectionStart;
    let end = textarea.selectionEnd;
    textarea.value = textarea.value.substring(0, start) + "\t" + textarea.value.substring(end);
}

</script>

<template>
    <textarea id="textarea" 
    v-text="modelValue" 
    @keydown.tab.prevent="onTabPress"
    @keyup="emit('update:modelValue', $event.target.value)"
    ></textarea>
</template>
```
