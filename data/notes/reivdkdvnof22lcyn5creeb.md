## Composition Over Inheretance

Is the principle that classes should achieve polymorphic behavior and code reuse by their composition (by containing instances of other classes that implement the desired functionality) rather than inheritance from a base or parent class. This is an often-stated principle of OOP, such as in the influential book Design Patterns (1994).

## SOLID JavaScript

- Single Responsibility Principle
- Open/Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

### S - Single Responsibility

States that a class (or object or module.. you get the point) should only have one responsibility. This doesn’t mean that an object can only do one thing, but it does mean that everything an object does should be part of one responsibility.

A class should have only one reason to change:

This description can be a little misleading as it would seem to suggest that an object should only do one thing. What is meant by this assertion, however, is that an object should have a cohesive set of behaviors, together comprising a single responsibility that, if changed, would require the modification of the object’s definition.  More simply, an object’s definition should only have to be modified due to changes to a single responsibility within the system.

#### Object Role Stereotypes

One approach which can aid in the organization of behavior within a system is the use of Object Role Stereotypes.  Object Role Stereotypes are a set of general, pre-established roles which commonly occur across object-oriented architectures.  By establishing a set of role stereotypes, developers can provide themselves with a set of templates which they can use as they go through the mental exercise of decomposing behavior into cohesive components.

- Information holder – an object designed to know certain information and provide that information to other objects.
- Structurer – an object that maintains relationships between objects and information about those relationships.
- Service provider – an object that performs specific work and offers services to others on demand.
- Controller – an object designed to make decisions and control a complex task.
- Coordinator – an object that doesn’t make many decisions but, in a rote or mechanical way, delegates work to other objects.
- Interfacer – an object that transforms information or requests between distinct parts of a system.

While not prescriptive, this set of role stereotypes provides an excellent mental framework for aiding in the software design process.  Once you have an established  set of role stereotypes to work within, you’ll find it easier to group behaviors into cohesive groups of responsibilities related to the object’s intended role.

### O - Open-Closed Principle

Open-Closed Principle means our JavaScript modules should be open to extension, but closed to modification.

Meaning that if someone wants to extend our module’s behavior, they won’t need to modify existing code if they don’t want to.

There’s a very easy rule of thumb you can follow here. If I have to open the JS file your module and make a modification in order to extend it, you’ve failed the open closed principle.

### L - Liskov Substitution Principle

The Liskov substitution principle (LSP) is a particular definition of a subtyping relation, called strong behavioral subtyping, that was initially introduced by Barbara Liskov in a 1988 conference keynote address titled Data abstraction and hierarchy. It is based on the concept of "substitutability" – a principle in object-oriented programming stating that an object (such as a class) and a sub-object (such as a class that extends the first class) must be interchangeable without breaking the program. It is a semantic rather than merely syntactic relation, because it intends to guarantee semantic interoperability of types in a hierarchy, object types in particular.

A great example illustrating LSP was how sometimes something that sounds right in natural language doesn't quite work in code.

In mathematics, a Square is a Rectangle. Indeed it is a specialization of a rectangle. The "is a" makes you want to model this with inheritance. However if in code you made Square derive from Rectangle, then a Square should be usable anywhere you expect a Rectangle. This makes for some strange behavior.

Imagine you had `SetWidth` and `SetHeight` methods on your `Rectangle` base class; this seems perfectly logical. However if your `Rectangle` reference pointed to a `Square`, then `SetWidth` and `SetHeight` doesn't make sense because setting one would change the other to match it. In this case Square fails the Liskov Substitution Test with `Rectangle` and the abstraction of having `Square` inherit from Rectangle is a bad one.

For example, if `MySubclass` is a subclass of `MyClass`, you should be able to replace `MyClass` with `MySubclass` without bunging up the program.

### I - Interface Segregation

Clients should not be forced to depend on methods they do not use.

When clients depend upon objects which contain methods used only by other clients, or are forced to implement unused methods with degenerate functionality (potentially leading to Liskov Substitution Principle violations), this can lead to fragile code. This occurs when an object serves as an implementation for a non-cohesive interface.

The Interface Segregation Principle is similar to the Single Responsibility Principle in that both deal with the cohesion of responsibilities. In fact, the ISP can be understood as the application of the SRP to an object’s public interface.

### - Dependency Inversion Principle

Dependency Injection and Inversion of Controls also mean the same thing. This is the most famous principle out of the bunch.

Dependency Injection is all about handing over control from the function itself to the caller of the function. In our case its defining who controls the type of parameters the function receives.

A. High-level modules should not depend on low-level modules. Both should depend on abstractions.

B. Abstractions should not depend upon details.  Details should depend upon abstractions.

The primary concern of the Dependency Inversion Principle is to ensure that the main components of an application or framework remain decoupled from the ancillary components providing low-level implementation details.  This ensures that the important parts of an application or framework aren’t affected when the low level components need to change.

Bad:

```javascript
function awesomeSauce(dispatcher) {
  dispatcher.trigger('awesome/sauce');
}

function awesomeSauceListener(dispatcher) {
  dispatcher.on('awesome/sauce', () => {
    alert('awesome!');
  });
}
```

Good:

```javascript
function awesomeSauce(dispatch) {
  dispatch('awesome/sauce');
}

function awesomeSauceListener(listen) {
  listen('awesome/sauce', () => {
    alert('awesome!');
  });
}
```

## Publish / Subscribe Pattern

In software architecture, publish–subscribe is a messaging pattern where senders of messages, called publishers, do not program the messages to be sent directly to specific receivers, called subscribers, but instead categorize published messages into classes without knowledge of which subscribers, if any, there may be. Similarly, subscribers express interest in one or more classes and only receive messages that are of interest, without knowledge of which publishers, if any, there are.

Publish–subscribe is a sibling of the message queue paradigm, and is typically one part of a larger message-oriented middleware system. Most messaging systems support both the pub/sub and message queue models in their API; e.g., Java Message Service (JMS).

This pattern provides greater network scalability and a more dynamic network topology, with a resulting decreased flexibility to modify the publisher and the structure of the published data.
