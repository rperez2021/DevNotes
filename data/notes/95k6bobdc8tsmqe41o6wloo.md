## General Info

Modules are actually very similar to factory functions. The main difference is how they’re created.

```javascript
const calculator = (() => {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  return {
    add,
    sub,
    mul,
    div,
  };
})();

calculator.add(3,5); // 8
calculator.sub(6,2); // 4
calculator.mul(14,5534); // 77476
```

The concepts are exactly the same as the factory function. However, instead of creating a factory that we can use over and over again to create multiple objects, the module pattern wraps the factory in an IIFE (Immediately Invoked Function Expression) [[devnotes.javascript.iife]].

The Module Pattern is one of the most common design patterns used in JavaScript and for good reason. The module pattern is easy to use and creates encapsulation of our code. Modules are commonly used as singleton style objects where only one instance exists. The Module Pattern is great for services and testing/TDD.

## Creating a Module

Start with an anonymous closure. Anonymous closures are just functions that wrap our code and create an enclosed scope around it. Closures help keep any state or privacy within that function. Closures are one of the best and most powerful features of JavaScript.

```javascript
(function() {
  'use strict';
  // Your code here
  // All function and variables are scoped to this function
})();
```

This pattern is well known as a Immediately Invoked Function Expression or IIFE. The function is evaluated then immediately invoked. Its also a good practice to run your modules in ES5 strict mode. Strict mode will protect you from some of the more dangerous parts in JavaScript.

## Exporting a Module

This basically assigns the module to a variable that we can use to call our modules methods.

```javascript
var myModule = (function() {
  'use strict';

})();
```

Next lets create a public method for our module to call. To expose this method to code outside our module we return an Object with the methods defined.

```javascript
var myModule = (function() {
  'use strict';

  return {
    publicMethod: function() {
      console.log('Hello World!');
    }
  };
})();

myModule.publicMethod(); // outputs 'Hello World'
```

## Private Methods and Properties

JavaScript does not have a private keyword by default but using closures we can create private methods and private state.

```javascript
var myModule = (function() {
  'use strict';

  var _privateProperty = 'Hello World';

  function _privateMethod() {
    console.log(_privateProperty);
  }

  return {
    publicMethod: function() {
      _privateMethod();
    }
  };
})();

myModule.publicMethod(); // outputs 'Hello World'
console.log(myModule._privateProperty); // is undefined protected by the module closure
myModule._privateMethod(); // is TypeError protected by the module closure
```

Because our private properties are not returned they are not available outside of our module. Only our public method has given us access to our private methods. This gives us ability to create private state and encapsulation within our code.

You may have noticed the _ before our private methods and properties. Because JavaScript does not have a private keyword its common to prefix private properties with an underscore.

## Revealing Module Pattern

The Revealing Module Pattern is one of the most popular ways of creating modules. Using the return statement we can return a object literal that 'reveals' only the methods or properties we want to be publicly available.

```javascript
var myModule = (function() {
  'use strict';

  var _privateProperty = 'Hello World';
  var publicProperty = 'I am a public property';

  function _privateMethod() {
    console.log(_privateProperty);
  }

  function publicMethod() {
    _privateMethod();
  }

  return {
    publicMethod: publicMethod,
    publicProperty: publicProperty
  };
})();

myModule.publicMethod(); // outputs 'Hello World'
console.log(myModule.publicProperty); // outputs 'I am a public property'
console.log(myModule._privateProperty); // is undefined protected by the module closure
myModule._privateMethod(); // is TypeError protected by the module closure
```

The benefit to the Revealing Module Pattern is that we can look at the bottom of our modules and quickly see what is publicly available for use.

The Module Pattern is not a silver bullet for adding code re-usability to your JavaScript. Using the Module Pattern with Prototypal Inheritance or ES6 Classes can give you a wide range of design patterns with varying pros and cons.

## require.resolve('some_module')

The command `require.resolve('some_module')` will show you the path to the module that node finds as a result of the tree climbing process.
