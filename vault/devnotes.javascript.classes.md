---
id: 6h8zgrpkw9ux59gwco02z4s
title: Classes
desc: 'JavaScript Classes'
updated: 1648496353667
created: 1648496353667
---
## General Info

Introduced in ES6 with the `class` keyword.

JavaScript provides a very flexible object system without the need to rely on `class`. So why did we add `class` in the first place? Because a lot of people are familiar with the class paradigm from other languages, and people kept trying to emulate it in JavaScript.

>Inheritance in JavaScript is so easy, it confuses people who expect it to >take effort. To make it harder, we added `class`.

Several popular libraries implemented pseudo-class inheritance in JavaScript using the delegate prototype chain to emulate class inheritance. Adding an official `class` keyword provided a single canonical way to emulate class inheritance in JavaScript — but in my opinion, you should avoid it altogether.

In JavaScript, composition is simpler, more expressive, and more flexible than class inheritance. I can’t think of a single good use case where `class` is a better fit than the native prototypal alternatives.

Once you start thinking in terms of class-free objects and inheritance using prototypes, and concatenation, you begin to really appreciate how simple, powerful, and flexible JavaScript’s object system can be.

```javascript
class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

// Usage:
let user = new User("John");
user.sayHi();
```

> No comma between class methods
> A common pitfall for novice developers is to put a comma between class methods, which would result in a syntax error.
>The notation here is not to be confused with object literals. Within the class, no commas are required.

### What is a class?

What class User {...} construct really does is:

1. Creates a function named User, that becomes the result of the class declaration. The function code is taken from the constructor method (assumed empty if we don’t write such method).
2. Stores class methods, such as sayHi, in User.prototype.

### Hoisting

An important difference between function declarations and class declarations is that while functions can be called in code that appears before they are defined, classes must be defined before they can be constructed. Code like the following will throw a ReferenceError:

```javascript
const p = new Rectangle(); // ReferenceError

class Rectangle {}
```

### Not Just Syntactic Sugar

Sometimes people say that class is a “syntactic sugar” (syntax that is designed to make things easier to read, but doesn’t introduce anything new), because we could actually declare the same thing without using the class keyword at all.

Still, there are important differences.

1. First, a function created by class is labelled by a special internal property `[[IsClassConstructor]]`: true. So it’s not entirely the same as creating it manually. The language checks for that property in a variety of places. For example, unlike a regular function, it must be called with `new`

2. Class methods are non-enumerable. A class definition sets `enumerable` flag to false for all methods in the "prototype". That’s good, because if we for..in over an object, we usually don’t want its class methods.

3. Classes always use strict. All code inside the class construct is automatically in strict mode.

### Class Expression

Here is a class expression:

```javascript
let User = class {
  sayHi() {
    alert("Hello");
  }
};
```

If a class expression has a name, it’s visible inside the class only:

```javascript
// "Named Class Expression"
// (no such term in the spec, but that's similar to Named Function Expression)
let User = class MyClass {
  sayHi() {
    alert(MyClass); // MyClass name is visible only inside the class
  }
};

new User().sayHi(); // works, shows MyClass definition

alert(MyClass); // error, MyClass name isn't visible outside of the class
```

We can even make classes dynamically “on-demand”, like this:

```javascript
function makeClass(phrase) {
  // declare a class and return it
  return class {
    sayHi() {
      alert(phrase);
    }
  };
}

// Create a new class
let User = makeClass("Hello");

new User().sayHi(); // Hello
```

### Getters and Setters in Classes

Just like literal objects, classes may include getters/setters, computed properties etc.

```javascript
class User {

  constructor(name) {
    // invokes the setter
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short.");
      return;
    }
    this._name = value;
  }

}

let user = new User("John");
alert(user.name); // John

user = new User(""); // Name is too short.
```

#### Computed Names

Here’s an example with a computed method name using brackets [...]:

```javascript
class User {

  ['say' + 'Hi']() {
    alert("Hello");
  }

}

new User().sayHi();
```

### Class Fields

> Old browsers may need a polyfill

“Class fields” is a syntax that allows to add any properties.

Previously, our classes only had methods.

“Class fields” is a syntax that allows to add any properties.

The important difference of class fields is that they are set on individual objects, not User.prototype:

```javascript
class User {
  name = "John";

  sayHi() {
    alert(`Hello, ${this.name}!`);
  }
}

new User().sayHi(); // Hello, John!
alert(user.name); // John
alert(User.prototype.name); // undefined
```

#### Bound Methods with Class Fields

As demonstrated in the chapter Function binding functions in JavaScript have a dynamic this. It depends on the context of the call.

So if an object method is passed around and called in another context, this won’t be a reference to its object any more.

For instance, this code will show undefined:

```javascript
class Button {
  constructor(value) {
    this.value = value;
  }

  click() {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // undefined
```

The problem is called "losing this".

There are two approaches to fixing it, as discussed in the chapter Function binding:

1. Pass a wrapper-function, such as `setTimeout(() => button.click(), 1000)`.
2. Bind the method to object, e.g. in the constructor.

Class fields provide another, quite elegant syntax:

```javascript
class Button {
  constructor(value) {
    this.value = value;
  }
  click = () => {
    alert(this.value);
  }
}

let button = new Button("hello");

setTimeout(button.click, 1000); // hello
```

The class field click = () => {...} is created on a per-object basis, there’s a separate function for each Button object, with this inside it referencing that object. We can pass button.click around anywhere, and the value of this will always be correct.

That’s especially useful in browser environment, for event listeners.

### Static Initialization Blocks

Class static initialization blocks allow flexible initialization of class static properties including the evaluation of statements during initialization, and granting access to private scope.

Multiple static blocks can be declared, and these can be interleaved with the declaration of static properties and methods (all static items are evaluated in declaration order).

```javascript
class ClassWithStaticInitializationBlock {
  static staticProperty1 = 'Property 1';
  static staticProperty2;
  static {
    this.staticProperty2 = 'Property 2';
  }
}

console.log(ClassWithStaticInitializationBlock.staticProperty1);
// output: "Property 1"
console.log(ClassWithStaticInitializationBlock.staticProperty2);
// output: "Property 2"
```

### Static Methods and Properties

The static keyword defines a static method or property for a class. Static members (properties and methods) are called without instantiating their class and **cannot** be called through a class instance. Static methods are often used to create utility functions for an application, whereas static properties are useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances.

### Sub classing with extends

The extends keyword is used in class declarations or class expressions to create a class as a child of another class.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name); // call the super class constructor and pass in the name parameter
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}

let d = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```

If there is a constructor present in the subclass, it needs to first call super() before using "this".

One may also extend traditional function-based "classes":

```javascript
function Animal (name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log(`${this.name} makes a noise.`);
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

let d = new Dog('Mitzie');
d.speak(); // Mitzie barks.

// For similar methods, the child's method takes precedence over parent's method
```

### Mixin's

Abstract subclasses or mix-ins are templates for classes. An ECMAScript class can only have a single superclass, so multiple inheritance from tooling classes, for example, is not possible. The functionality must be provided by the superclass.

A function with a superclass as input and a subclass extending that superclass as output can be used to implement mix-ins in ECMAScript:

```javascript
let calculatorMixin = Base => class extends Base {
  calc() { }
};

let randomizerMixin = Base => class extends Base {
  randomize() { }
};
```

A class that uses these mix-ins can then be written like this:

```javascript
class Foo { }
class Bar extends calculatorMixin(randomizerMixin(Foo)) { }
```
