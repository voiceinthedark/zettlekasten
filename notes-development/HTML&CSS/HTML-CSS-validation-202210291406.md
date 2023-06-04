---
title: HTML-CSS-validation
date: 29/10/2022
tags: html css validation regex
---

# **HTML-CSS-validation** 202210291406 <!-- omit in toc -->
> **b88f07**

- [the required validation](#the-required-validation)
- [Text Length validation](#text-length-validation)
  - [Min length](#min-length)
  - [Max length](#max-length)
  - [Combining validations](#combining-validations)
- [Number Range validation](#number-range-validation)
  - [min range](#min-range)
  - [max range](#max-range)
- [Pattern validation](#pattern-validation)
- [Styling validations](#styling-validations)
  
## the required validation
To make a field required, we simply add the `required` attribute to it`.

## Text Length validation

### Min length
To add the minimum length validation, we give the form control a `minlength` attribute with an integer value that represents the minimum amount of characters we want to allow in the form control.
```html
<div>
    <textarea placeholder="What's happening?" minlength="3"></textarea>
  </div>
```
### Max length
To add a maximum length validation, we give the form control a `maxlength` attribute with an integer value which represents the maximum amount of characters we want to allow in the form control`.

```html
<div>
    <textarea placeholder="What's happening?" maxlength="20"></textarea>
  </div>
```

### Combining validations
```html
<textarea placeholder="What's happening?" minlength="5" maxlength="20"></textarea>
```

## Number Range validation

### min range
```html
<input type="number" id="quantity" name="quantity" min="1" value="0">
```

### max range
```html
<input type="number" id="passengers" name="passengers" max="5" value="0">
```
## Pattern validation
To add a pattern validation, we give the form control a pattern attribute with a regular expression as the value.

```html
<input type="text" id="zip_code" name="zip_code" pattern="(\d{5}([\-]\d{4})?)" required>
```
We can add a more descriptive validation message by giving our input a title attribute:
```html
<input type="text" id="zip_code" name="zip_code" pattern="(\d{5}([\-]\d{4})?)" title="Please enter a valid zip code, example: 65251" required>
```

## Styling validations
We can target form controls that have passed or failed validations using the :valid and :invalid pseudo-classes.

```css

input {
  border: 2px solid #000;
  margin-bottom: 15px;
  padding: 5px;
  border-radius: 5px;
}

input:invalid {
  border-color: red;
}

input:valid {
  border-color: green;
}```

