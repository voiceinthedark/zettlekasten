---
title: vue-components
date: 19/07/2023
tags: vue component
---

# **vue-components** 202307190556 
> **0f6d7e**

## Basic component

```javascript
 <div id="app">
      <app-button>Hi there</app-button>
    </div>

    <script>
      const component = {
        components: {
          'app-button': {
            template: `<button class="px-4 py-2 font-bold text-white bg-blue-500 rounded hover:bg-blue-700">
            <slot />
            </button>`,
          },
        },
      };

      const app = Vue.createApp(component);
      app.mount('#app');
    </script>
```

## Setting up components props

```javascript
/** inside AppButton.js */
export default {
  template: `<button 
  :class="{
    'px-4 py-2 font-bold text-black border' : true,
    'bg-red-500 hover:bg-red-700 text-white' : type === 'danger',
    'bg-green-500 hover:bg-green-700 text-white' : type === 'success',
    'bg-blue-500 hover:bg-blue-700 text-white' : type === 'info',
  }"
  :disabled="processing"
  >
              <slot />
            </button>`,
  props: {
    processing: {
      type: Boolean,
      default: false,
    },
    type: {
      type: String,
      default: 'info',
    },
  },
};

```
<hr>

```javascript
/** Inside App.js */
import AppButton from './AppButton.js';
export default {
  components: {
    'app-button': AppButton,
  },
};
```
<hr>

```html
/** Inside html.index */
<div id="app">
      <app-button type="danger">Submit</app-button>
    </div>

    <script type="module">
      import App from './js/components/App.js';

      Vue.createApp(App).mount('#app');
    </script>
```

## Logical seperation
It is a important to seperate chunks of code into multiple components.
  where each component is its own file, and each component is a smaller chunk of code that belongs to a parent component.

### Example
```javascript
/** main html file */
<div id="app">
      <assignments></assignments>
    </div>

    <script type="module">
      import App from './js/components/App.js';

      Vue.createApp(App).mount('#app');
    </script>
```

<hr>

```javascript
/** main js file */
import Assignments from './Assignments.js';
export default {
  components: {
    assignments: Assignments,
  },
};
```
<hr>

```javascript
/** Assignments.js */
import AssignmentList from './AssignmentList.js';

export default {
  components: {
    'assignment-list': AssignmentList,
  },
  template: `
      <section class="space-y-2">
          <assignment-list :assignments="filters.incomplete" title="Incomplete Assignments"></assignment-list>
          <assignment-list :assignments="filters.completed" title="Completed Assignments"></assignment-list>
      </section>
    `,
  data() {
    return {
      assignments: [
        { name: 'Homework', completed: false },
        { name: 'Projects', completed: false },
        { name: 'Train Harder', completed: false },
      ],
    };
  },
  computed: {
    filters() {
      return {
        completed: this.assignments.filter(
          (assignment) => assignment.completed
        ),
        incomplete: this.assignments.filter(
          (assignment) => !assignment.completed
        ),
      };
    },
  },
};
```

<hr>

```javascript
/** AssignmentList.js */
import Assignment from './Assignment.js';
export default {
    components: {
        'assignment': Assignment        
    },
  template: `
    <section v-show="assignments.length > 0">
        <h1 class="mb-2 font-bold">{{ title }}</h1>
        <ul>
            <assignment v-for="assignment in assignments" :key="assignment.name" :assignment="assignment"></assignment>
        </ul>
      </section>
      `,

      props: {
          assignments: {
              type: Array,
              required: true
          },
          title: {
              type: String,
              required: true
          }
      }
};
```

<hr>

```javascript
/** Assignment.js */
export default{
    template: `
    <li>
            <label>
              {{assignment.name}}
              <input type="checkbox" v-model="assignment.completed" />
            </label>
          </li>
    `,
    props: {
        assignment: {
            type: Object,
            required: true
        }
    }
}
```


