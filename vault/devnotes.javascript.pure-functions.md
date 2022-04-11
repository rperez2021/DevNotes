---
id: 1rqugxsqrzodsifdbrujgcu
title: Pure Functions
desc: 'Notes on Pure Functions'
updated: 1649696222083
created: 1649695782436
---
## What is a pure function

1. The function always returns the same result if the same arguments are passed in. It does not depend on any state, or data, change during a program’s execution. It must only depend on its input arguments.
2. The function does not produce any observable side effects such as network requests, input and output devices, or data mutation.

## What are Observable Side Effects

**Note**: If a pure function calls a pure function this isn’t a side effect and the calling function is still pure.

Side effects include, but are not limited to:

- Making a HTTP request
- Mutating data
- Printing to a screen or console
- DOM Query/Manipulation
- Math.random()
- Getting the current time

### Pure Function Example

```javascript
function priceAfterTax(productPrice) {
 return (productPrice * 0.20) + productPrice;
}
```

It passes both 1, and 2, of the requirements for a function to be declared pure. It doesn’t depend on any external input, it doesn’t mutate any data and it doesn’t have any side effects.

### Impure Function Example

```javascript
var tax = 20;
function calculateTax(productPrice) {
 return (productPrice * (tax/100)) + productPrice; 
}
```

A pure function can not depend on outside variables. It fails one of the requirements thus this function is impure.

## Why Are Pure Functions Important In JavaScript?

Not all functions need to be , or should be, pure. For example, an event handler for a button press that manipulates the DOM is not a good candidate for a pure function. But, the event handler can call other pure functions which will reduce the number of impure functions in your application.

### Testability And Refactoring

One of the major benefits of using pure functions is they are immediately testable. They will always produce the same result if you pass in the same arguments.

They also makes maintaining and refactoring code much easier. You can change a pure function and not have to worry about unintended side effects messing up the entire application and ending up in debugging hell.

When used correctly the use of pure functions produces better quality code. It’s a cleaner way of working with lots of benefits.

Note that pure functions are not limited to JavaScript. For an in depth — mind numbing — explanation of pure functions see here. I also highly recommend reading this and this.
