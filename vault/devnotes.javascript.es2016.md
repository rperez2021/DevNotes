---
id: tjiwvr8nu9v64rrgbyy54u3
title: Es2016
desc: 'ES2016 Notes'
updated: 1649274581630
created: 1649274449033
---
## List of Changes

Just two changes:

1. Array.prototype.includes
2. Exponentiation Operator

### Array.prototype.includes()

With ES6 and lower, to check if an array contained an element you had to use indexOf, which checks the index in the array, and returns -1 if the element is not there.

Since -1 is evaluated as a true value, you could not do for example

```javascript
if (![1,2].indexOf(3)) {
  console.log('Not found')
}
```

With this feature introduced in ES2016 we can do

```javascript
if (![1,2].includes(3)) {
  console.log('Not found')
}
```

### Exponentiation Operator **

The exponentiation operator ** is the equivalent of Math.pow(), but brought into the language instead of being a library function.

```javascript
Math.pow(4, 2) == 4 ** 2
```

