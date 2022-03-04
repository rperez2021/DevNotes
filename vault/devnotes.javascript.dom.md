---
id: ifx9x9mx76ipl6ballgoxyz
title: Dom
desc: 'Notes About the DOM'
updated: 1646260795644
created: 1646256849423
---
## General Info

### Relational Selectors

[Documentation can be found here](https://developer.mozilla.org/en-US/docs/Web/API/Element)

Examples:

previousElementSibling

firstElementChild

It’s important to note that when using querySelectorAll, the return value is not an array. It looks like an array, and it somewhat acts like an array, but it’s really a “nodelist”. The big distinction is that several array methods are missing from nodelists. One solution, if problems arise, is to convert the nodelist into an array. You can do this with Array.from() or the spread operator.
