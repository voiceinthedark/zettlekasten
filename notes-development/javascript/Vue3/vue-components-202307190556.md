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
### Parent-child interactions
Parent sends data to childs through props. A child should send data to parent
  through event emission.

```javascript
/** Parent */
import AssignmentList from './AssignmentList.js';
import AssignmentCreate from './AssignmentCreate.js';

export default {
  components: {
    'assignment-list': AssignmentList,
    'assignment-create': AssignmentCreate,
  },
  template: `
      <section class="space-y-2 ">
          <assignment-list :assignments="filters.incomplete" title="Incomplete Assignments"></assignment-list>
          <assignment-list :assignments="filters.completed" title="Completed Assignments"></assignment-list>
      </section>

      <assignment-create @add-assignment="addAssignment"></assignment-create>
      
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

  methods: {
    addAssignment(name) {
      this.assignments.push({ name: name, completed: false });
    },
  }
};
```

```javascript
/** Child */
export default {
  template: `
    <form class="mt-2 text-black" @submit.prevent="addAssignment">
          <input class="p-2" type="text" v-model="newAssignment" />
          <button class="p-2 bg-white border-l" type="submit">Add Assignment</button>
      </form>
    `,

    data() {
      return {
        newAssignment: '',
      };
    },
    methods: {
        addAssignment() {
            // Emit event to parent
            this.$emit('add-assignment', this.newAssignment);
        }
    }
};
```

## Putting it all together

We are using the `modelValue` prop to pass data from child to parent.
Our event emission should hold the form of `update:propname`:

```javascript
/** AssignmentTags.js */
export default {
  template: `
    <div class= "flex-row px-1 inline-flex" v-for="tag in tags">
            <button @click.prevent="$emit('update:currentTag', tag)" class="border px-1 rounded"
            :class="{ 'border-blue-600': currentTag === tag }"
            >{{ tag }}</button>
        </div>
    `,

  props: {
    currentTag: {
      type: String,
      required: true,
    },
    assignments: {
      type: Array,
      required: true,
    },
    currentTag: {
      type: String,
      required: true,
    },
  },
  emits: ['update:currentTag'],
  computed: {
    tags() {
      return ['all', ...new Set(this.assignments)];
    },
  },
};
```

Then on the parent component we bind the prop to a v-model to a custom component. It takes this form `v-model:propname`, we don't need to listen to
  the custom event here, since v-model will take care of that behind the scene.

```javascript
/** AssignmentList.js */
import Assignment from './Assignment.js';
import AssignmentTags from './AssignmentTags.js';

export default {
  components: {
    'assignment': Assignment,
    'assignment-tags': AssignmentTags,
  },
  template: `
    <section v-show="assignments.length > 0">
        <h1 class="mb-2 font-bold">
        {{ title }}
        ({{ assignments.length }})
        </h1>

        <assignment-tags v-model:currentTag="currentTag"
        :assignments="assignments.map(a => a.tag)"
        ></assignment-tags>


        <ul class="mt-3 border border-gray-500 divide-y divide-gray-500">
            <assignment v-for="assignment in filteredAssignments" :key="assignment.name" :assignment="assignment"></assignment>
        </ul>
      </section>      
      `,

  props: {
    assignments: {
      type: Array,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    
  },
  
  data() {
    return {
      currentTag: 'all',
    };
  },

  computed:{
    
    filteredAssignments(){
      return this.currentTag === 'all' ? this.assignments : this.assignments.filter(assignment => assignment.tag === this.currentTag)
    }
  }
};
```
