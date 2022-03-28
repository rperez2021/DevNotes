---
id: kqruud4o7klnncek6cnf9pd
title: Factory_functions
desc: Notes on Factory Functions
updated: 1648483981910
created: 1648483981910
---
## General Info

The factory function pattern is similar to constructors, but instead of using `new` to create an object, factory functions simply set up and return the new object when you call the function.

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

## Inheritance with factories

Example of how to inheret a function property with factory functions.

```javascript
const Person = (name) => {
  const sayName = () => console.log(`my name is ${name}`);
  return {sayName};
}

const Nerd = (name) => {
  // simply create a person and pull out the sayName function with destructuring assignment syntax!
  const {sayName} = Person(name);
  const doSomethingNerdy = () => console.log('nerd stuff');
  return {sayName, doSomethingNerdy};
}

const jeff = Nerd('jeff');

jeff.sayName(); //my name is jeff
jeff.doSomethingNerdy(); // nerd stuff
```

If you want to inheret all methods you can use the `Object.assign` method:

```javascript
const Nerd = (name) => {
  const prototype = Person(name);
  const doSomethingNerdy = () => console.log('nerd stuff');
  return Object.assign({}, prototype, {doSomethingNerdy});
}
```
