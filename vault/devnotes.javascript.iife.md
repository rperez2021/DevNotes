---
id: xw8fc28leh6h0o4q51ju5br
title: IIFE
desc: 'Immediately Invoked Function Expression'
updated: 1648496758889
created: 1648496758889
---
## General Information

It doesn't take very long working with JavaScript before you come across this pattern:

```javascript
(function () {
    // logic here
})();
```

The primary reason to use an IIFE is to obtain data privacy. Because JavaScript's var scopes variables to their containing function, any variables declared within the IIFE cannot be accessed by the outside world.

Of course, you could explicitly name and then invoke a function to achieve the same ends.

However, this approach has a few downsides. First, it unnecessarily takes up a name in the global namespace, increasing the possibility of name collisions. Second, the intentions of this code aren't as self-documenting as an IIFE. And third, because it is named and isn't self-documenting it might accidentally be invoked more than once.

It is worth pointing out that you can easily pass arguments into the IIFE as well.
