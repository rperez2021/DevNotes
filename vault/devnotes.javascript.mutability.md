---
id: x87g82j1wxd2xaehc5qurlh
title: Mutability
desc: 'Notes on Mutability in JS'
updated: 1650151243141
created: 1650149904968
---
## General Info

JavaScript offers several ways to add, remove, and replace items in an array – but some of these ways mutate the array, and others are non-mutating; they produce a new array.

- `array.splice()` mutates the original array
- `array.slice()` does not mutate the original array

### Addition with Mutation

The mutating methods for adding to an array are `array.push()` which adds an item to the end of the array and `array.ushift()` which adds an item to the beginning of the array..

```javascript
// since the array will be mutated, 
// use 'let' rather than 'const'
let mutatingAdd = ['a', 'b', 'c', 'd', 'e']; 

mutatingAdd.push('f'); // ['a', 'b', 'c', 'd', 'e', 'f']
mutatingAdd.unshift('z'); // ['z', 'a', 'b', 'c', 'd', 'e' 'f']
```

### Addition without Mutation

The non-mutating method `array.concat()` is one way

```javascript
// since we will not be mutating, 
// use const
const arr1 = ['a', 'b', 'c', 'd', 'e'];

const arr2 = arr1.concat('f'); // ['a', 'b', 'c', 'd', 'e'. 'f']
console.log(arr1); // ['a', 'b', 'c', 'd', 'e']
```

Using the `...spread` operator is another:

```javascript
// since we will not be mutating, 
// use const
const arr1 = ['a', 'b', 'c', 'd', 'e'];

const arr2 = [...arr1, 'f']; // ['a', 'b', 'c', 'd', 'e', 'f']
const arr3 = ['z', ...arr1]; // ['z', 'a', 'b', 'c', 'd', 'e']
```

### Removal with Mutation

The mutating methods for removing from an array are `array.pop()` which removes an item at the end of the array, `array.shift()` which removes an item at the beginning of the array and `array.splice()` which can accept several parameters.

```javascript
// since the array will be mutated, 
// use 'let' rather than 'const'
let mutatingRemove = ['a', 'b', 'c', 'd', 'e'];
mutatingRemove.pop(); // ['a', 'b', 'c', 'd']
mutatingRemove.shift(); // ['b', 'c', 'd']
```

`array.pop()` and `array.shift()` return the item that is removed. This means you can 'catch' the deleted item in a variable.

1. The first parameter is the starting point of the splice.
2. The second parameter is the number of items to remove from the array.
3. The third parameter can be used to add items in the place of the removes items.

Like array.pop() and array.shift(), array.splice() returns the items it removes.

```javascript
let mutatingRemove = ['a', 'b', 'c', 'd', 'e'];
let returnedItems = mutatingRemove.splice(0, 2);
console.log(mutatingRemove); // ['c', 'd', 'e']
console.log(returnedItems) // ['a', 'b'] 
```

### Removal without Mutating

JavaScript's `array.filter()` method creates a new array from an original array, but the new array only contains items that match the specified criteria. Another way is with `array.slice()` **Dont Confuse with `array.splice()`**

```javascript
// since we will not be mutating, 
// use const
const arr1 = ['a', 'b', 'c', 'd', 'e'];

const arr2 = arr1.filter(a => a !== 'e'); // ['a', 'b', 'c', 'd']
// OR
const arr2 = arr1.filter(a => {
  return a !== 'e';
}); // ['a', 'b', 'c', 'd']
```

`array.slice()` takes two parameters.

1. The first parameter is the index where the copy should begin.
2. The second parameter is the index where the copy should end. This end index is non-inclusive.

```javascript
// since we will not be mutating, 
// use const
const arr1 = ['a', 'b', 'c', 'd', 'e'];
const arr2 = arr1.slice(1, 5) // ['b', 'c', 'd', 'e']
const arr3 = arr1.slice(2) // ['c', 'd', 'e']
```

Line 5 `(const arr3 = arr1.slice(2))` shows a handy trick. If the second parameter of array.slice() is not provided, the method makes a copy from the beginning index to the end of the array.

### Replacing with Mutation

If you know the index of the item you want to replace, you can use `array.splice()` to replace it with something else.

In order to do this, we need to use at least three parameters:

1. The first parameter is the index to start replacing.
2. The second parameter is the number of items to remove.
3. The third and all other parameters are what will be inserted into the array.

```javascript
// since the array will be mutated, 
// use 'let' rather than 'const'
let mutatingReplace = ['a', 'b', 'c', 'd', 'e'];
mutatingReplace.splice(2, 1, 30); // ['a', 'b', 30, 'd', 'e']
// OR
mutatingReplace.splice(2, 1, 30, 31); // ['a', 'b', 30, 31, 'd', 'e']
```

### Replace without Mutating

We can use `array.map()` to create a new array, but we can also check each item and replace items that match a specified criterion.

```javascript
// since we will not be mutating, 
// use const
const arr1 = ['a', 'b', 'c', 'd', 'e']
const arr2 = arr1.map(item => {
  if(item === 'c') {
    item = 'CAT';
  }
  return item;
}); // ['a', 'b', 'CAT', 'd', 'e']
```

The code above creates a new array based on arr1, but replaces all 'c's with CATs.

### Transforming Data with `array.map()`

`array.map()` is a powerful method, and can be used to transform data without compromising the integrity of the original data set.

```javascript
// since we will not be mutating, 
// use const
const origArr = ['a', 'b', 'c', 'd', 'e'];
const transformedArr = origArr.map(n => n + 'Hi!'); // ['aHi!', 'bHi!', 'cHi!', 'dHi!', 'eHi!']
// OR
const transformedArr = origArr.map(n => {
  return n * 2;
})// ['aHi!', 'bHi!', 'cHi!', 'dHi!', 'eHi!']
console.log(origArr); // ['a', 'b', 'c', 'd', 'e']; // orignal array is intact
```
