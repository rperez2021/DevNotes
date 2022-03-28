---
id: 6h8zgrpkw9ux59gwco02z4s
title: Classes
desc: 'JavaScript Classes'
updated: 1648496353667
created: 1648496353667
---
## General Info

JavaScript provides a very flexible object system without the need to rely on `class`. So why did we add `class` in the first place? Because a lot of people are familiar with the class paradigm from other languages, and people kept trying to emulate it in JavaScript.

>Inheritance in JavaScript is so easy, it confuses people who expect it to >take effort. To make it harder, we added `class`.

Several popular libraries implemented pseudo-class inheritance in JavaScript using the delegate prototype chain to emulate class inheritance. Adding an official `class` keyword provided a single canonical way to emulate class inheritance in JavaScript — but in my opinion, you should avoid it altogether.

In JavaScript, composition is simpler, more expressive, and more flexible than class inheritance. I can’t think of a single good use case where `class` is a better fit than the native prototypal alternatives.

Once you start thinking in terms of class-free objects and inheritance using prototypes, and concatenation, you begin to really appreciate how simple, powerful, and flexible JavaScript’s object system can be.
