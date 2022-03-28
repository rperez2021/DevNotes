---
id: imj2klai3czrmnvx416fjqk
title: Method Delegation Inheretance
desc: Another Word for Prototypal Inheretance
updated: 1648494442158
created: 1648494442158
---
## Method Delegation (Prototypal Inheretance or Class Inheretance)

[[devnotes.javascript.objects.prototype]]

### ES6 Class Constructor Version

```javascript
class Greeter {
  constructor (name) {
    this.name = name || 'John Doe';
  }
  hello () {
    return `Hello, my name is ${ this.name }`;
  }
}

const george = new Greeter('George');

const msg = george.hello();
 
console.log(msg); // Hello, my name is George
```

### ES5 Constructor Function Version

```javascript
function Greeter (name) {
  this.name = name || 'John Doe';
}

Greeter.prototype.hello = function hello () {
  return 'Hello, my name is ' + this.name;
}

var george = new Greeter('George');

var msg = george.hello();

console.log(msg); // Hello, my name is George
```

### Factory Function Version

```javascript
const proto = {
  hello () {
    return `Hello, my name is ${ this.name }`;
  }
};

const greeter = (name) => Object.assign(Object.create(proto), {
  name
});

const george = greeter('george');

const msg = george.hello();

console.log(msg);
```

## Composition Over Class Inheretance

Class inheritance creates is-a relationships with restrictive taxonomies, all of which are eventually wrong for new use-cases. But it turns out, we usually employ inheritance for has-a, uses-a, or can-do relationships.

Composition is more like a guitar effects pedalboard. Want something that can do delay, subtle distortion, and a robot voice? No problem! Just plug them all in:

```javascript
const effect = compose(delay, distortion, robovoice); // Rock on!
```

Composition is:

1. Simple
2. More expressive
3. More flexible
