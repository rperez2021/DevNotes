---
id: viploue6ww80cf7iueemp5k
title: Prototype
desc: Notes on Javascript Object Prototypes
updated: 1648353547406
created: 1648353547406
---
## General Info

**Prototype Property**: Every JavaScript function has a prototype property that is empty by default.

**Prototype Attribute**: Think of the prototype attribute as a characteristic of the object; this characteristic tells us the object’s “parent”.

**Constructor**: is a function used for initializing new objects, and you use the new keyword to call the constructor.

**Prototype Property: Prototype-based Inheritance (Prototypal inheritance)**: In JavaScript, you implement inheritance with the prototype property. For example, you can create a Fruit function (an object, since all functions in JavaScript are objects) and add properties and methods on the Fruit prototype property, and all instances of the Fruit function will inherit all the Fruit’s properties and methods.

```javascript
// Explicitly Passing Inheretance
Fruit.prototype = new Plant ();

// Another way, you probably shouldnt do it like this but you can:
let animal = {
  eats: true,
  walk() {
    alert("Animal walk");
  }
};

let rabbit = {
  jumps: true,
  __proto__: animal
};

// walk is taken from the prototype
rabbit.walk(); // Animal walk

```

**Prototype Attribute: Accessing Properties on Objects**: prototype attribute (or prototype object) of any object is the “parent” object where the inherited properties were originally defined.

If the property is not found on the object’s prototype, the search for the property then moves to prototype of the object’s prototype (the father of the object’s father—the grandfather). And this continues until there is no more prototype (no more great-grand father; no more lineage to follow).

This in essence is the **prototype chain:** the chain from an object’s prototype to its prototype’s prototype and onwards.

If the property does not exist on any of the object’s prototype in its prototype chain, then the property does not exist and undefined is returned.

This prototype chain mechanism is essentially the same concept we have discussed above with the prototype-based inheritance, except we are now focusing specifically on how JavaScript accesses object properties and methods via the prototype object.

**Object.prototype Properties Inherited by all Objects**: All objects in JavaScript inherit properties and methods from Object.prototype. These inherited properties and methods are:

1. `constructor`
2. `hasOwnProperty()`
3. `isPrototypeOf()`
4. `propertyIsEnumerable()`
5. `toLocaleString()`
6. `toString()`
7. `valueOf()`
8. ECMAScript 5 also adds 4 accessor methods to Object.prototype.

### Prototypal Inheretance

[[devnotes.javascript.objects.method-delegation-inheretance]]

### Limitations on Prototypal Inheretance

1. References cant go in circles. JavaScript will throw an error if we try to assign `__proto__` in a circle.
2. The value of `__proto__` can be either an object or null. Other types are ignored.

### The Getter / Setter Exception

There is an exception to how Prototypal Inheretance functions with getters and setters, because they are functions using them is the same as using a function from the prototype.

### How 'this' functions

This is not affected by prototypes at all.

No matter where the method is found: in an object or its prototype. In a method call, this is always the object before the dot.

That is actually a super-important thing, because we may have a big object with many methods, and have objects that inherit from it. And when the inheriting objects run the inherited methods, they will modify only their own states, not the state of the big object.

### Utilizing For...in loops

`Object.keys(objName)` will only return the keys associated with objName

but a for...in loop will return both its own keys and its inhereted keys

```javascript
for(let property in objName) alert(property);
```

if you only want to return an objects own properties (exclude prototype props) there is a buil in JS method called `obj.hasOwnProperty(key)` which returns `true` if the object has the property.

You can use a for loop to filter like so:

```javascript
let animal = {
  eats: true
};

let rabbit = {
  jumps: true,
  __proto__: animal
};

for(let prop in rabbit) {
  let isOwn = rabbit.hasOwnProperty(prop);

  if (isOwn) {
    alert(`Our: ${prop}`); // Our: jumps
  } else {
    alert(`Inherited: ${prop}`); // Inherited: eats
  }
}
```

### Enumerable Flag in Protoypes

Like all other properties of Object.prototype, it has enumerable:false flag. And for..in only lists enumerable properties. That’s why it and the rest of the Object.prototype properties are not listed.

### Recommended Method for Prototypal Inheretance

The recommended way of setting the prototype of an object is `Object.create`(here is the documentation for that method). Object.create very simply returns a new object with the specified prototype and any additional properties you want to add.
