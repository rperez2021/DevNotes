---
id: 9bfos5omm2d2kdv5wo0vhk3
title: ES2017
desc: 'ES2017 Notes'
updated: 1649281728082
created: 1649274214843
---
## List of Changes

- String padding
- Object.values()
- Object.entries()
- Object.getOwnPropertyDescriptors()
- Trailing commas in function parameter lists and calls
- Async functions
- Shared memory and atomics

### String Padding

The purpose of string padding is to add characters to a string, so it reaches a specific length.

`padStart(targetLength [, padString])`

`padEnd(targetLength [, padString])`

Sample usage:

```javascript
padStart()	
‘test’.padStart(4)	// ‘test’
‘test’.padStart(5)	// ‘ test’
‘test’.padStart(8)	// ‘    test’
‘test’.padStart(8, ‘abcd’)	// ‘abcdtest’

padEnd()	
‘test’.padEnd(4)  //	‘test’
‘test’.padEnd(5)	// ‘test ‘
‘test’.padEnd(8)	// ‘test    ‘
‘test’.padEnd(8,  // ‘abcd’)	‘testabcd’
```

### Object.values()

This method returns an array containing all the object own property values.

Usage:

```javascript
const person = { name: 'Fred', age: 87 }
Object.values(person) // ['Fred', 87]
Object.values() 

// also works with arrays!:

const people = ['Fred', 'Tony']
Object.values(people) // ['Fred', 'Tony']
```

### Object.entries()

This method returns an array containing all the object own properties, as an array of [key, value] pairs.

Usage:

```javascript
const person = { name: 'Fred', age: 87 }
Object.entries(person) // [['name', 'Fred'], ['age', 87]]
Object.entries() 

//also works with arrays:

const people = ['Fred', 'Tony']
Object.entries(people) // [['0', 'Fred'], ['1', 'Tony']]
```

### getOwnPropertyDescriptors()

This method returns all own (non-inherited) properties descriptors of an object.

Any object in JavaScript has a set of properties, and each of these properties has a descriptor.

A descriptor is a set of attributes of a property, and it’s composed by a subset of the following:

- value: the value of the property
- writable: true the property can be changed
- get: a getter function for the property, called when the property is read
- set: a setter function for the property, called when the property is set to a value
- configurable: if false, the property cannot be removed nor any attribute can be changed, except its value
- enumerable: true if the property is enumerable

`Object.getOwnPropertyDescriptors(obj)` accepts an object, and returns an object with the set of descriptors.
