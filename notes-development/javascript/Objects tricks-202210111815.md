---
title: Objects tricks
date: 11/10/2022
tags: javascript object
---

# **Objects tricks** 202210111815 
> **6d1f51**

  

- Object packing and unpacking:
```javascript
    function addName(obj, name, value) {
	return {...obj, [name]: value}	
    }
```