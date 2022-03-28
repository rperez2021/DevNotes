---
id: sfau59x9kshetjbln41f9ta
title: Scope
desc: ''
updated: 1648485164360
created: 1648485164360
---
## Namespace

The namespace is sometimes an interchangeable word for scope, but usually the refers to the highest level scope.

## Root Scope

Root Scope is Window

so a root variable like:

```javascript
var a = 1
// can be accessed by:
window.a
// which will return 
1
```

## Naming Conflict

```javascript
var a = 1;

function foo() {
    var a = 2;
    console.log(a)
    // will return 2 because connection to root a is broken
}

foo();
```

## Lexical Scope

Lexical scope is easy to work with, any variables/objects/functions defined in its parent scope, are available in the scope chain. The only important thing to remember is that Lexical scope does not work backwards.

## Closure

Closures ties in very closely with Lexical Scope. A better example of how the closure side of things works, can be seen when returning a function reference - a more practical usage.

A function doesn’t have to return in order to be called a closure though. Simply accessing variables outside of the immediate lexical scope creates a closure.

## Scope and ‘this’

Each scope binds a different value of this depending on how the function is invoked. We’ve all used the this keyword, but not all of us understand it and how it differs when invoked. By default this refers to the outer most global object, the window. We can easily show how invoking functions in different ways binds the this value differently:

```javascript
var myFunction = function () {
  console.log(this); // this = global, [object Window]
};
myFunction();

var myObject = {};
myObject.myMethod = function () {
  console.log(this); // this = Object { myObject }
};

var nav = document.querySelector('.nav'); // <nav class="nav">
var toggleNav = function () {
  console.log(this); // this = <nav> element
};
nav.addEventListener('click', toggleNav, false);
```

There are also problems that we run into when dealing with the this value, for instance if I do this, even inside the same function the scope can be changed and the this value can be changed:

```javascript
var nav = document.querySelector('.nav'); // <nav class="nav">
var toggleNav = function () {
  console.log(this); // <nav> element
  setTimeout(function () {
    console.log(this); // [object Window]
  }, 1000);
};
nav.addEventListener('click', toggleNav, false);
```

So what’s happened here? We’ve created new scope which is not invoked from our event handler, so it defaults to the window Object as expected. There are several things we can do if we want to access the proper this value which isn’t affected by the new scope. You might have seen this before, where we can cache a reference to the this value using a that variable and refer to the lexical binding:

```javascript
var nav = document.querySelector('.nav'); // <nav class="nav">
var toggleNav = function () {
  var that = this;
  console.log(that); // <nav> element
  setTimeout(function () {
    console.log(that); // <nav> element
  }, 1000);
};
nav.addEventListener('click', toggleNav, false);
```

This is a neat little trick to be able to use the proper this value and resolve problems with newly created scope.

## Changing scope with .call(), .apply() and .bind()

The .call() and .apply() methods are really sweet, they allows you to pass in a scope to a function, which binds the correct this value. Let’s manipulate the above function to make it so that our this value is each element in the array:

```javascript
var links = document.querySelectorAll('nav li');
for (var i = 0; i < links.length; i++) {
  (function () {
    console.log(this);
  }).call(links[i]);
}
```

You can see I’m passing in the current element in the Array iteration, links[i], which changes the scope of the function so that the this value becomes that iterated element. We can then use the this binding if we wanted. We can use either .call() or .apply() to change the scope, but any further arguments are where the two differ: .call(scope, arg1, arg2, arg3) takes individual arguments, comma separated, whereas .apply(scope, [arg1, arg2]) takes an Array of arguments.

It’s important to remember that using .call() or .apply() actually invokes your function, so instead of doing this:

```javascript
myFunction(); // invoke myFunction
```

You’ll let .call() handle it and chain the method:

```javascript
myFunction.call(scope); // invoke myFunction using .call()
```

### .bind()

Unlike the above, using .bind() does not invoke a function, it merely binds the values before the function is invoked. It’s a real shame this was introduced in ECMAScript 5 and not earlier as this method is fantastic.

```javascript
nav.addEventListener('click', toggleNav.bind(scope, arg1, arg2), false);
```

## Private and Public Scope

In many programming languages, you’ll hear about public and private scope, in JavaScript there is no such thing. We can, however, emulate public and private scope through things like Closures.

By using JavaScript design patterns, such as the Module pattern for example, we can create public and private scope. A simple way to create private scope, is by wrapping our functions inside a function. As we’ve learned, functions create scope, which keeps things out of the global scope:

```javascript
(function () {
  // private scope inside here
})();
```

We might then add a few functions for use in our app:

```javascript
(function () {
  var myFunction = function () {
    // do some stuff here
  };
})();
```

But when we come to calling our function, it would be out of scope:

```javascript
(function () {
  var myFunction = function () {
    // do some stuff here
  };
})();

myFunction(); // Uncaught ReferenceError: myFunction is not defined
```

Success! We’ve created private scope. But what if I want the function to be public? There’s a great pattern (called the Module Pattern [and Revealing Module Pattern]) which allows us to scope our functions correctly, using private and public scope and an Object. Here I grab my global namespace, called Module, which contains all of my relevant code for that module:

```javascript
// define module
var Module = (function () {
  return {
    myMethod: function () {
      console.log('myMethod has been called.');
    }
  };
})();

// call module + methods
Module.myMethod();
```

The return statement here is what returns our public methods, which are accessible in the global scope - but are namespaced. This means our Module takes care of our namespace, and can contain as many methods as we want. We can extend the Module as we wish:

```javascript
// define module
var Module = (function () {
  return {
    myMethod: function () {

    },
    someOtherMethod: function () {

    }
  };
})();

// call module + methods
Module.myMethod();
Module.someOtherMethod();
```

So what about private methods? This is where a lot of developers go wrong and pollute the global namespace by dumping all their functions in the global scope. Functions that help our code work do not need to be in the global scope, only the API calls do - things that need to be accessed globally in order to work. Here’s how we can create private scope, by not returning functions:

```javascript
var Module = (function () {
  var privateMethod = function () {

  };
  return {
    publicMethod: function () {

    }
  };
})();
```

This means that publicMethod can be called, but privateMethod cannot, as it’s privately scoped! These privately scoped functions are things like helpers, addClass, removeClass, Ajax/XHR calls, Arrays, Objects, anything you can think of.

Here’s an interesting twist though, anything in the same scope has access to anything in the same scope, even after the function has been returned. Which means, our public methods have access to our private ones, so they can still interact but are unaccessible in the global scope.

```javascript
var Module = (function () {
  var privateMethod = function () {

  };
  return {
    publicMethod: function () {
      // has access to `privateMethod`, we can call it:
      // privateMethod();
    }
  };
})();
```

This allows a very powerful level of interactivity, as well as code security. A very important part of JavaScript is ensuring security, which is exactly why we can’t afford to put all functions in the global scope as they’ll be publicly available, which makes them open to vulnerable attacks.

Here’s an example of returning an Object, making use of public and private methods:

```javascript
var Module = (function () {
  var myModule = {};
  var privateMethod = function () {

  };
  myModule.publicMethod = function () {

  };
  myModule.anotherPublicMethod = function () {

  };
  return myModule; // returns the Object with public methods
})();

// usage
Module.publicMethod();
```

One neat naming convention is to begin private methods with an underscore, which visually helps you differentiate between public and private:

```javascript
var Module = (function () {
  var _privateMethod = function () {

  };
  var publicMethod = function () {

  };
})();
```

This helps us when returning an anonymous Object, which the Module can use in Object fashion as we can simply assign the function references:

```javascript
var Module = (function () {
  var _privateMethod = function () {

  };
  var publicMethod = function () {

  };
  return {
    publicMethod: publicMethod,
    anotherPublicMethod: anotherPublicMethod
  }
})();
```

## Source

I grabbed most of these notes from this guide:

[Everything You Wanted to Know About JS Scope](https://ultimatecourses.com/blog/everything-you-wanted-to-know-about-javascript-scope)
