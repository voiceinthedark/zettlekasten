---
title: sending-data-from-a-vue-to-a-persistent-layout
date: 07/08/2023
updated_at: 2023-08-07T08:53:04.534Z
tags: vue vuejs inertia laravel php 
---

# **sending-data-from-a-vue-to-a-persistent-layout** 202308071152 
> **6c01ff**

## The Problem

During development of my personal blog, I wanted to send data from my 
vue Page to the persistent layout of my entire site. 
  The problem here is that my vue page is not a traditional parent-child component; 
rather due to my choice of a persistent layout instead of a default layout, 
the layout is decoupled naturally, from the rest of the Pages on my site, 
which reside in the dedicated default slot of my Layout.

Typically my layout is persistent through the main configuration of inertia:


**app.js**{title="app.js"}
```javascript
createInertiaApp({
    resolve: (name) =>
    {// set default layout
        const page = resolvePageComponent(
            `./Pages/${name}.vue`,
            import.meta.glob("./Pages/**/*.vue")
        );
        page.then((component) => {
            component.default.layout = component.default.layout || Layout;
        });
        return page;
    },
});
```
There is no way to interact with the persistent layout from the vue page, since they are decoupled.
This is intentional, since this allows the layout and the pages to be rendered independently.

## Possible solutions
Figuring out the problem is the first step; unfortunately find a viable solution takes many more steps.
The [consensus](https://github.com/inertiajs/inertia/issues/176) was the use of the `eventBus` to communicate between the two.[^1]
This unfortunately requires a lot of boilerplate code and doesn't seem to work with Vue 3.

## A workaround
The only viable solution is to use a custom event bus, or a store to communicate between the two.
This at least has the benefit of two way communication.

**useSharedStore.js**{title="useSharedStore.js"}
```javascript
import { reactive } from 'vue'

export const store = reactive({
    // Store the content of the TOC
    sharedData: null,  // [!code focus]
    // Store the active heading
    activeHeading: null,
})

```

After that we have to store the data we need to send to the persistent layout.

**Article.vue**{title="Article.vue"}
```javascript
function extractTOC(article) {
    // Create a DOMParser object to parse the article's body as HTML.
    let parser = new DOMParser();

    // Parse the article's body as HTML and store the resulting document in the 'doc' variable.
    let doc = parser.parseFromString(article.body, "text/html");

    // Select all elements with the class 'table-of-contents' from the parsed document and store them in the 'toc' variable.
    let toc = doc.querySelectorAll(".table-of-contents");

    // Store the table of contents in the sharedData property of the store object.
    store.sharedData = toc && toc.length > 0 ? toc.item(0).outerHTML : ""; // [!code hl]
    // console.log(store.sharedData);
}
```
I am trying to use the `extractTOC` function to extract the TOC from an article, like this one
    and send it to the main layout in order to pass it to a side layout which will display it as a table of contents for the aforementioned article.

We then receive the data in the persistent layout, like this:

**Layout.vue**{title="Layout.vue"}
```javascript
let tableOfContents = ref(null);

watch(
    () => store.sharedData,
    (newVal) => {
        tableOfContents.value = newVal;
    }
);
```

And then we simply pass it to the side layout as a prop:

**Layout.vue**{title="Layout.vue"}
```javascript
<aside>
    <SideLayout :toc="tableOfContents" />
</aside>
```

## A Diagram of the solution

> The solution diagram

```mermaid
%%{init: {'theme': "neutral"}}%%
stateDiagram-v2
    [*] --> Extract_TOC
    Extract_TOC --> Send_TOC_TO_Persistent_Layout
    Extract_TOC --> Store_TOC_IN_Shared_Store
    Send_TOC_TO_Persistent_Layout --> Store_TOC_IN_Shared_Store
    Store_TOC_IN_Shared_Store --> Send_TOC_TO_Persistent_Layout
    Send_TOC_TO_Persistent_Layout --> Send_TOC_TO_Side_Layout
    Send_TOC_TO_Side_Layout --> [*]
```

Until next time. :wolf:  

[^1]: [digital ocean global event bus](https://www.digitalocean.com/community/tutorials/vuejs-global-event-bus)  

