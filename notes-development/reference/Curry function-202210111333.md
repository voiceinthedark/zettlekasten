---
title: Curry function
date: 11/10/2022
tags: javascript functional-programming fp curry-functions
---

# **Curry function** 202210111333 
> **77ae4f**

  

A currying function (named after mathematician Haskell Curry) is a function that splits
input into sub functions.

```javascript
    function add(x, y) {
        return x + y;
    }
    /* This function curryed becomes: */
    function add(x){
        return new function(y){
            return x + y;
        }
    }
    /* Or more compactly: */
    const add = (x) => (y) => x + y;
```