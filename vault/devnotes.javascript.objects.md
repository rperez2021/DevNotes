---
id: viufua5jjzuuans4ncdrz9m
title: Objects
desc: Notes on JavaScript Objects
updated: 1646761459795
created: 1646692621428
---
## General Info

Objects are sometimes called Associative Arrays

functions in objects (methods) do not need to be separated by a colon they can be shorthand written just as the function name.

```javascript
let user = {
    name: "John Smith"
    introduceSelf: function() {
        console.log(`Hi! I'm ${this.name[0]}.`);
    }
}

// can also be written as
let user = {
    name: "John Smith"
    introduceSelf() {
        console.log(`Hi! I'm ${this.name[0]}.`);
    }
}
```

### The IN operator

While you can check to see if a key is undefined to find out wether it exists or not there is the chance that the value in the key may actually be undefined and would therefore come back as true. The IN operator allows you to check for the existance of a key without worrying if its value is undefinedd.

### The "for... in" loop

To iterate over object keys theres a special for in loop with the following syntax:

```javascript
// this function will return true is an object is empty false if not
function isEmpty(obj) {
    for (let key in obj) {
        return false
    }
    return true
}
```

### Constructors

- Start with a capital letter and are named for the type of object they create

```javascript
function Person(name) {
  this.name = name;
  this.introduceSelf = function() {
    console.log(`Hi! I'm ${this.name}.`);
  }
}

// to call a Person() as a constructor we use new

const salva = new Person('Salva');
salva.name;
salva.introduceSelf();

const frankie = new Person('Frankie');
frankie.name;
frankie.introduceSelf();
```
