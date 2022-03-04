---
id: 0kUgAtckpQ0Nk0ClNqfcE
title: Arrays
desc: 'Notes on JS Arrays'
updated: 1645729706226
created: 1645670170208
---
## General Notes

`Array.isArray()` was created because there is no typeof property for arrays since they are typeof `objects`

Weird stuff happens when you use an array constructor for a single item in an array.

```javascript
const points = new Array(40, 100, 1);
points
[40, 100, 1

const points2 = [40, 100, 1]
points
[40, 100, 1]

const points3 = new Array(40)
points
[ <40 empty items> ]

const points4 = [40]
points
[ 40 ]
```

## Array Methods

### Converting Arrays to Strings

`.toString()` converts an array into a comma separated string

`.join(separator)` also converts an array into a string and you can specify the separator as a parameter.

JavaScript automatically converts an array to a comma separated string when a primitive value is expected. Without needing to call the `.toString()` method

### Popping and Pushing

`.pop(element)` removes the last element

`.push(element)` adds an element to the end of the array

### Shifting Elements

`.shift()` removes the first element and shifts the others to the left, it also returns the element that was shifted out

`.unshift()` adds a new element at the beginning of the array and returns the new array length

### Changing Elements

`.length` easy way to append an element to an array, also provides the length of an array

`delete array[0]` will delete the element but leave an `undefined` hole

`.concat()` will combine any number of arrays or strings

`.splice()` can be used to add new items to the array ex:

```javascript
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
```

`.slice(start, end)` slices out a piece of an array into a new array but does not modify the old array.

```javascript
const fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
const citrus = fruits.slice(1);
citrus = [ 'Orange', 'Lemon', 'Apple', 'Mango' ]
fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"]
```

