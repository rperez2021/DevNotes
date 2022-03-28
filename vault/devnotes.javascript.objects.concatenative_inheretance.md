---
id: 6he4kwf3y255bqrmzdqllrb
title: Concatenative_inheretance
desc: 'JS Object Concatenative Inheretance or Cloning'
updated: 1648495041735
created: 1648495041735
---
## Definition

Concatenative inheritance is the process of copying the properties from one object to another, without retaining a reference between the two objects. It relies on JavaScript’s dynamic object extension feature.

Cloning is a great way to store default state for objects: This process is commonly achieved using `Object.assign()`. Prior to ES6, it was common to use similar `.extend()` methods from Lodash, Underscore, or jQuery.

```javascript
const proto = {
  hello: function hello() {
    return `Hello, my name is ${ this.name }`;
  }
};

const george = Object.assign({}, proto, {name: 'George'});

const msg = george.hello();

console.log(msg); // Hello, my name is George
```

It’s common to see this style used for mixins. For example, you can turn any object into an event emitter by mixing in an `EventEmitter3` prototype:

```javascript
import Events from 'eventemitter3';

const object = {};

Object.assign(object, Events.prototype);

object.on('event', payload => console.log(payload));

object.emit('event', 'some data'); // 'some data'
```

Concatenative inheritance is very powerful, but it gets even better when you combine it with closures.

## Functional Inheretance and Functional Mixins

Functional inheritance makes use of a factory function, and then tacks on new properties using concatenative inheritance.

Functions created for the purpose of extending existing objects are commonly referred to as functional mixins. The primary advantage of using functions for extension is that it allows you to use the function closure to encapsulate private data. In other words, you can enforce private state.

It’s a bit awkward to hang the attributes on a public property where a user could set or get them without calling the proper methods. What we really want to do is hide the attributes in a private closure. It looks something like this:

```javascript
import Events from 'eventemitter3';

const rawMixin = function () {
  const attrs = {};

  return Object.assign(this, {
    set (name, value) {
      attrs[name] = value;

      this.emit('change', {
        prop: name,
        value: value
      });
    },

    get (name) {
      return attrs[name];
    }
  }, Events.prototype);
};

const mixinModel = (target) => rawMixin.call(target);

const george = { name: 'george' };
const model = mixinModel(george);

model.on('change', data => console.log(data));

model.set('name', 'Sam');
/*
{
  prop: 'name',
  value: 'Sam'
}
*/
```

By moving `attrs` from a public property to a private identifier, we remove all trace of it from the public API. The only way to use it now is via the **privileged methods**.

### Priviliged Methods

**Privileged methods** are any methods defined within the closure’s function scope, which gives them access to the private data.

Note in the example above, we have the `mixinModel()` wrapper around the actual functional mixin, `rawMixin()`. The reason we need that is because we need to set the value of `this` inside the function, which we do with `Function.prototype.call()`. We could skip the wrapper and let callers do that instead, but that would be obnoxious.
