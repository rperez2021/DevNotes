## General Info

```javascript
function Apple(color, weight) {
    this.color = color;
    this.weight = weight;
}
```

If you’re using constructors to make your objects it is best to define functions on the prototype of that object. Doing so means that a single instance of each function will be shared between all of the Student objects. If we declare the function directly in the constructor, like we did when they were first introduced, that function would be duplicated every time a new Student is created.

## Recommended Method for Prototypal Inheretance

The recommended way of setting the prototype of an object is Object.create (here is the documentation for that method). Object.create very simply returns a new object with the specified prototype and any additional properties you want to add. For our purposes, you use it like so:

```javascript
function Student() {
}

Student.prototype.sayName = function() {
  console.log(this.name)
}

function EighthGrader(name) {
  this.name = name
  this.grade = 8
}

EighthGrader.prototype = Object.create(Student.prototype)

const carl = new EighthGrader("carl")
carl.sayName() // console.logs "carl"
carl.grade // 8
```

After creating the constructor for EighthGrader, we set its prototype to a new object that has a copy of Student.prototype.

A warning… this doesn’t work:

```javascript
EighthGrader.prototype = Student.prototype
```

## Constructor Method in Classes

The constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name "constructor" in a class. A SyntaxError will be thrown if the class contains more than one occurrence of a constructor method.

A constructor can use the super keyword to call the constructor of the super class.
