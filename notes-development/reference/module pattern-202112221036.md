---
title: module pattern
date: 22/12/22
tags: design-patterns javascript module
---

# **module pattern** 202112221036 
> **815aa9**

  
## Revealing Module Pattern

A variation of the module pattern is called the **Revealing Module Pattern**. The purpose is to maintain encapsulation and reveal certain variables and methods returned in an object literal. The direct implementation looks like this:

```javascript
var Exposer = (function() {
    var privateVariable = 10;

    var privateMethod = function() {
    console.log('Inside a private method!');
    privateVariable++;
    }

    var methodToExpose = function() {
    console.log('This is a method I want to expose!');
    }

    var otherMethodIWantToExpose = function() {
    privateMethod();
    }

    return {
        first: methodToExpose,
        second: otherMethodIWantToExpose
    };
})();

Exposer.first();        // Output: This is a method I want to expose!
Exposer.second();       // Output: Inside a private method!
Exposer.methodToExpose; // undefined
```
