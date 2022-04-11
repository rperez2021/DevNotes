---
id: g85a34yzexx39qwx21jt1d1
title: ES2018
desc: 'ES2018 Release Notes'
updated: 1649378580196
created: 1649366191513
---
## List of New Features

- Rest/Spread Properties
- Asynchronous iteration
- `Promise.prototype.finally()`
- Regular Expression improvements
  - RegExp lookbehind assertions: match a string depending on what precedes it
  - Unicode property escapes `\p{…}` and `\P{…}`
  - Named capturing groups
  - The `s` flag for regular expressions

### Rest/Spread Properties

ES6 introduced the concept of a rest element when working with array destructuring:

```javascript
const numbers = [1, 2, 3, 4, 5]
[first, second, ...others] = numbers
and spread elements:

const numbers = [1, 2, 3, 4, 5]
const sum = (a, b, c, d, e) => a + b + c + d + e
const sumOfNumbers = sum(...numbers)
```

ES2018 introduces the same but for objects.

Rest properties:

```javascript
const { first, second, ...others } = { first: 1, second: 2, third: 3, fourth: 4, fifth: 5 }

first // 1
second // 2
others // { third: 3, fourth: 4, fifth: 5 }
```

Spread properties allow to create a new object by combining the properties of the object passed after the spread operator:

```javascript
const items = { first, second, ...others }
items //{ first: 1, second: 2, third: 3, fourth: 4, fifth: 5 }
```
