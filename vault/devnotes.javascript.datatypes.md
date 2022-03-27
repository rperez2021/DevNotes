---
id: jMwhka851RbdJKAoiQWxK
title: Data Types
desc: Explanation of JavaScript Data Types
updated: 1644558898703
created: 1644557871912
---

## General Info

There are 8 data types, the first six are called *primitives*:

1. **Numbers** (Interger or Floating Point)

2. **BigInt** - is created by appending a **n** to the end of an integer.

3. **String** - created by ```" ", ' ', ` ` ```

4. **Boolean** - true or false

5. **"null"** value - in JS represents "nothing", "empty" or "unknown"

6. **"undefined"** value - "value is not assigned"

7. **Object** - for complex data structures

8. **Symbol** - for unique identifiers

## Additional Notes

```typeof null``` returns ```"object"``` - That’s an officially recognized error in typeof, coming from very early days of JavaScript and kept for compatibility. Definitely, null is not an object. It is a special value with a separate type of its own. The behavior of typeof is wrong here.

```typeof alert``` returns ```function``` - There’s no special “function” type in JavaScript. Functions belong to the object type. But typeof treats them differently, returning "function". That also comes from the early days of JavaScript. Technically, such behavior isn’t correct, but can be convenient in practice.

```typeof``` is an operator not a function seeing ```typeof(x)``` is just syntactic sugar.
