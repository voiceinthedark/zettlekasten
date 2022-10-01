---
title: Console.log tips
date: 01/10/2022
tags: javascript console tips
---

# **Console.log tips** 202210012313 
> **25e86d**

- Console table:
```javascript
 /*Using console.table() on an array of objects will populate the data into a formatted table */
 console.table([{id: 1, name: 'jim'}, {id: 2, name: 'sim'}]);
```
- Console timer:
```js
  /* to use a timer in the console we use the console.time('timer-name') 
    and then close it with console.timeEnd('timer-name')
     when operation is done */
     console.time('fetchdata');
     fetch('url')
        .then(data => data.json())
        .then(data => {
            console.timeEnd('fetchdata');
            console.log(data);
        })
```
- Add css style to console log
```js
/* by superceding the log message with `%c` we can apply styles to the log */
console.log('%c This is a styled message', 'color: blue;');
```
- Grouping data in the console
```javascript
/* To group data during iteration we use the console.group() method*/
dogs.forEach(dog => {
    console.group(`${dog.name}`);
    console.log(`This is ${dog.name}`);
    console.log(`${dog.name} is ${dog.age} years old!`);
    console.groupEnd(`${dog.name}`);
});
```

