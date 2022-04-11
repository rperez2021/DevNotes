---
id: 44c7crm55o30cco7m146f2y
title: Aync Await
desc: 'Notes on JS Async Await'
updated: 1649378576656
created: 1649352637974
---
## General Info

An important thing to understand is async functions are just syntactical sugar for promises.

Asynchronous code can become difficult to follow when it has a lot of things going on. async and await are two keywords that can help make asynchronous read more like synchronous code. This can help code look cleaner while keeping the benefits of asynchronous code.

For example, the two code blocks below do the exact same thing. They both get information from a server, process it, and return a promise.

```javascript
function getPersonsInfo(name) {
  return server.getPeople().then(people => {
    return people.find(person => { return person.name === name });
  });
}
```

```javascript
async function getPersonsInfo(name) {
  const people = await server.getPeople();
  const person = people.find(person => { return person.name === name });
  return person;
}
```

### The Async Keyword

The `async` keyword can also be used with any of the ways a function can be created. Said differently: it is valid to use an `async` function anywhere you can use a normal function. Below you will see some examples that may not be intuitive. If you don’t understand them, come back and take a look when you are done with the assignments.

```javascript
const yourAsyncFunction = async () => {
    // do something asynchronously and return a promise
    return result;
  }

 anArray.forEach(async item => {
   // do something asynchronously for each item in 'anArray'
   // one could also use .map here to return an array of promises to use with 'Promise.all()'
 });
 
server.getPeople().then(async people => {
  people.forEach(person => {
    // do something asynchronously for each person
  });
});
```

### The Await Keyword

`await` is pretty simple: it tells JavaScript to wait for an asynchronous action to finish before continuing the function. It’s like a ‘pause until done’ keyword. The `await` keyword is used to get a value from a function where you would normally use `.then()`. Instead of calling `.then()` after the asynchronous function, you would simply assign a variable to the result using await. Then you can use the result in your code as you would in your synchronous code.

**Await accepts thenables**: Like `promise.then`, `await` allows us to use thenable objects (those with a callable then method). The idea is that a third-party object may not be a promise, but promise-compatible: if it supports `.then`, that’s enough to use it with await.

In modern browsers, await on top level works just fine, when we’re inside a module.

If we’re not using modules, or older browsers must be supported, there’s a universal recipe: wrapping into an anonymous async function.

### Error Handling

Handling errors in async functions is very easy. Promises have the `.catch()` method for handling rejected promises, and since async functions just return a promise, you can simply call the function, and append a `.catch()` method to the end.

```javascript
asyncFunctionCall().catch(err => {
  console.error(err)
});
```

But there is another way: the mighty try/catch block! If you want to handle the error directly inside the async function, you can use try/catch just like you would inside synchronous code.

```javascript
async function getPersonsInfo(name) {
  try {
    const people = await server.getPeople();
    const person = people.find(person => { return person.name === name });
    return person;
  } catch (error) {
    // Handle the error any way you'd like
  }
}
```

Doing this can look messy, but it is a very easy way to handle errors without appending `.catch()` after your function calls. How you handle the errors is up to you, and which method you use should be determined by how your code was written. You will get a feel for what needs to be done over time. The assignments will also help you understand how to handle your errors.
