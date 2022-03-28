---
id: kqruud4o7klnncek6cnf9pd
title: Factory Functions
desc: 'Notes on Factory Functions'
updated: 1648483981910
created: 1648483981910
---
## General Info

The factory function pattern is similar to constructors, but instead of using new to create an object, factory functions simply set up and return the new object when you call the function.

```javascript
const personFactory = (name, age) => {
  const sayHello = () => console.log('hello!');
  return { name, age, sayHello };
};

const jeff = personFactory('jeff', 27);

console.log(jeff.name); // 'jeff'

jeff.sayHello(); // calls the function and logs 'hello!'
```

### Object Shorthand

```javascript
// thanks to es6 this:
return {name: name, age: age, sayHello: sayHello};
// is the same as:
return {name, age, sayHello};
```

also this:

```javascript
const name = "Maynard";
const color = "red";
const number = 34;
const food = "rice";

// logging all of these variables might be a useful thing to do,
// but doing it like this can be somewhat confusing.
console.log(name, color, number, food); // Maynard red 34 rice

// if you simply turn them into an object with brackets,
// the output is much easier to decipher:
console.log({name, color, number, food});
 // { name: 'Maynard', color: 'red', number: 34, food: 'rice' }
 ```
