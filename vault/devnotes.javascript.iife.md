---
id: xw8fc28leh6h0o4q51ju5br
title: IIFE
desc: 'Immediately Invoked Function Expression'
updated: 1649272540533
created: 1648496758889
---
## General Information

An Immediately-invoked function expression, or IIFE (pronounced “iffy”), is a function expression (named or anonymous) that is executed right away after its creation.

It doesn't take very long working with JavaScript before you come across this pattern:

```javascript
(function () {
    // logic here
})();

// variant 2

(function () {
  alert('Woohoo!');
}());
```

## How To

1. You need to wrap the whole function in parentheses. As the name suggests, an IIFE must be a function expression, not a function definition. So, the purpose of the enclosing parentheses is to transform a function definition into an expression. This is because, in JavaScript, everything in parentheses is treated as an expression.
2. You need to add a pair of parentheses at the very end (variant 1), or right after the closing curly brace (variant 2), which causes the function to be executed immediately.
3. If you assign the function to a variable, you don’t need to enclose the whole function in parentheses, because it is already an expression:

    ```javascript
    var sayWoohoo = function () {
    alert('Woohoo!');
    }();
    ```

4. A semicolon is required at the end of an IIFE, as otherwise your code may not work properly.
5. You can pass arguments to an IIFE (it’s a function, after all), as the following example demonstrates:

    ```javascript
    (function (name, profession) {
    console.log("My name is " + name + ". I'm an " + profession + ".");
    })("Jackie Chan", "actor");   // output: My name is Jackie Chan. I'm an actor.
    ```

## Why

The primary reason to use an IIFE is to obtain data privacy. Because JavaScript's var scopes variables to their containing function, any variables declared within the IIFE cannot be accessed by the outside world.

Of course, you could explicitly name and then invoke a function to achieve the same ends.

However, this approach has a few downsides. First, it unnecessarily takes up a name in the global namespace, increasing the possibility of name collisions. Second, the intentions of this code aren't as self-documenting as an IIFE. And third, because it is named and isn't self-documenting it might accidentally be invoked more than once.

It is worth pointing out that you can easily pass arguments into the IIFE as well.

## Sources

[SitePoint Article](https://www.sitepoint.com/demystifying-javascript-closures-callbacks-iifes/)
