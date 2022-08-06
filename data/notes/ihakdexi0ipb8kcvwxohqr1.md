## General Info

The observer pattern is a software design pattern in which an object, named the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.

### What problems can the Observer design pattern solve?

The Observer pattern addresses the following problems:

- A one-to-many dependency between objects should be defined without making the objects tightly coupled.
- It should be ensured that when one object changes state, an open-ended number of dependent objects are updated automatically.
- It should be possible that one object can notify an open-ended number of other objects.

Defining a one-to-many dependency between objects by defining one object (subject) that updates the state of dependent objects directly is inflexible because it couples the subject to particular dependent objects. Still, it can make sense from a performance point of view or if the object implementation is tightly coupled (think of low-level kernel structures that execute thousands of times a second). Tightly coupled objects can be hard to implement in some scenarios, and hard to reuse because they refer to and know about (and how to update) many different objects with different interfaces. In other scenarios, tightly coupled objects can be a better option since the compiler will be able to detect errors at compile-time and optimize the code at the CPU instruction level.

### What solution does the Observer design pattern describe?

- Define Subject and Observer objects.
- so that when a subject changes state, all registered observers are notified and updated automatically (and probably asynchronously).

The sole responsibility of a subject is to maintain a list of observers and to notify them of state changes by calling their update() operation. The responsibility of observers is to register (and unregister) themselves on a subject (to get notified of state changes) and to update their state (synchronize their state with the subject's state) when they are notified. This makes subject and observers loosely coupled. Subject and observers have no explicit knowledge of each other. Observers can be added and removed independently at run-time. This notification-registration interaction is also known as publish-subscribe.
