---
title: Css-js-validation
date: 02/11/2022
tags: css javascript constraint-validation-api
---

# **Css-js-validation** 202211021243 
> **ad351a**

## JavaScript Form Validation

### [The Constraint Validation API](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation#test_your_skills!#the_constraint_validation_api "Permalink to The Constraint Validation API")

Most browsers support the [Constraint Validation API](https://developer.mozilla.org/en-US/docs/Web/API/Constraint_validation), which consists of a set of methods and properties available on the following form element DOM interfaces:

-   [`HTMLButtonElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLButtonElement) (represents a [`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button) element)
-   [`HTMLFieldSetElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFieldSetElement) (represents a [`<fieldset>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) element)
-   [`HTMLInputElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement) (represents an [`<input>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) element)
-   [`HTMLOutputElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLOutputElement) (represents an [`<output>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/output) element)
-   [`HTMLSelectElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLSelectElement) (represents a [`<select>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) element)
-   [`HTMLTextAreaElement`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLTextAreaElement) (represents a [`<textarea>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea) element)

The Constraint validation API makes the following properties available on the above elements.

-   `validationMessage`: Returns a localized message describing the validation constraints that the control doesn't satisfy (if any). If the control is not a candidate for constraint validation (`willValidate` is `false`) or the element's value satisfies its constraints (is valid), this will return an empty string.
-   `validity`: Returns a `ValidityState` object that contains several properties describing the validity state of the element. You can find full details of all the available properties in the [`ValidityState`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState) reference page; below is listed a few of the more common ones:
    -   [`patternMismatch`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/patternMismatch "patternMismatch"): Returns `true` if the value does not match the specified [`pattern`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-pattern), and `false` if it does match. If true, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) CSS pseudo-class.
    -   [`tooLong`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/tooLong "tooLong"): Returns `true` if the value is longer than the maximum length specified by the [`maxlength`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-maxlength) attribute, or `false` if it is shorter than or equal to the maximum. If true, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) CSS pseudo-class.
    -   [`tooShort`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/tooShort "tooShort"): Returns `true` if the value is shorter than the minimum length specified by the [`minlength`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-minlength) attribute, or `false` if it is greater than or equal to the minimum. If true, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) CSS pseudo-class.
    -   [`rangeOverflow`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/rangeOverflow "rangeOverflow"): Returns `true` if the value is greater than the maximum specified by the [`max`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-max) attribute, or `false` if it is less than or equal to the maximum. If true, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) and [`:out-of-range`](https://developer.mozilla.org/en-US/docs/Web/CSS/:out-of-range) CSS pseudo-classes.
    -   [`rangeUnderflow`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/rangeUnderflow "rangeUnderflow"): Returns `true` if the value is less than the minimum specified by the [`min`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-min) attribute, or `false` if it is greater than or equal to the minimum. If true, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) and [`:out-of-range`](https://developer.mozilla.org/en-US/docs/Web/CSS/:out-of-range) CSS pseudo-classes.
    -   [`typeMismatch`](https://developer.mozilla.org/en-US/docs/Web/API/ValidityState/typeMismatch "typeMismatch"): Returns `true` if the value is not in the required syntax (when [`type`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-type) is `email` or `url`), or `false` if the syntax is correct. If `true`, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) CSS pseudo-class.
    -   `valid`: Returns `true` if the element meets all its validation constraints, and is therefore considered to be valid, or `false` if it fails any constraint. If true, the element matches the [`:valid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:valid) CSS pseudo-class; the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) CSS pseudo-class otherwise.
    -   `valueMissing`: Returns `true` if the element has a [`required`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-required) attribute, but no value, or `false` otherwise. If true, the element matches the [`:invalid`](https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid) CSS pseudo-class.
-   `willValidate`: Returns `true` if the element will be validated when the form is submitted; `false` otherwise.

The Constraint Validation API also makes the following methods available on the above elements and the [`form`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) element.

-   `checkValidity()`: Returns `true` if the element's value has no validity problems; `false` otherwise. If the element is invalid, this method also fires an [`invalid` event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/invalid_event) on the element.
-   `reportValidity()`: Reports invalid field(s) using events. Useful in combination with `preventDefault()` in an `onSubmit` event handler
-   `setCustomValidity(message)`: Adds a custom error message to the element; if you set a custom error message, the element is considered to be invalid, and the specified error is displayed. This lets you use JavaScript code to establish a validation failure other than those offered by the standard HTML validation constraints. The message is shown to the user when reporting the problem.

