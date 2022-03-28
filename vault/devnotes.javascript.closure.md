---
id: 45uczs3eirc00ozni000aiw
title: Closure
desc: 'Notes on JS Closure Concept'
updated: 1648487756880
created: 1648487756880
---
## Example / Explanation

Closures ties in very closely with Lexical Scope. A better example of how the closure side of things works, can be seen when returning a function reference - a more practical usage. Inside our scope, we can return things so that they’re available in the parent scope:

```javascript
var sayHello = function (name) {
  var text = 'Hello, ' + name;
  return function () {
    console.log(text);
  };
};
```

The closure concept we’ve used here makes our scope inside sayHello inaccessible to the public scope. Calling the function alone will do nothing as it returns a function:

```javascript
sayHello('Todd'); // nothing happens, no errors, just silence...
```

The function returns a function, which means it needs assignment, and then calling:

```javascript
var helloTodd = sayHello('Todd');
helloTodd(); // will call the closure and log 'Hello, Todd'
```

Okay, I lied, you can call it, and you may have seen functions like this, but this will call your closure:

```javascript
sayHello('Bob')(); // calls the returned function without assignment
```

AngularJS uses the above technique for its $compile method, where you pass the current scope reference into the closure:

```javascript
$compile(template)(scope);
```

Meaning we could guess that their code would (over-simplified) look like this:

```javascript
var $compile = function (template) {
  // some magic stuff here
  // scope is out of scope, though...
  return function (scope) {
    // access to `template` and `scope` to do magic with too
  };
};
```

A function doesn’t have to return in order to be called a closure though. Simply accessing variables outside of the immediate lexical scope creates a closure.
