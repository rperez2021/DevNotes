---
id: 0h2im19vmn8wqa5tht9q8hm
title: React Hooks
desc: 'Notes on React Hooks'
updated: 1650775502035
created: 1650738091046
---
## General Info

Hooks allow functional components to also have a lifecycle as well as a state.

Imported as an object function from the React module:

```javascript
import React, { useState, useEffect } from "react";
```

Hooks were created as a way to solve these problems:

1. It’s hard to reuse stateful logic between components
    - Patterns like render props and higher-order components that try to solve this. But these patterns require you to restructure your components when you use them, which can be cumbersome and make code harder to follow
    - Hooks allow you to reuse stateful logic without changing your component hierarchy.
2. Complex components become hard to understand
    - Hooks let you split one component into smaller functions based on what pieces are related (such as setting up a subscription or fetching data)
3. Classes confuse both people and machines
    - You have to understand how this works in JavaScript, which is very different from how it works in most languages.
    - You have to remember to bind the event handlers.
    - Hooks let you use more of React’s features without classes.

## Hook Rules

1. Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.
2. Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks. We’ll learn about them in a moment.)

## Custom Hooks

Hooks are a way to reuse stateful logic, not state itself. In fact, each call to a Hook has a completely isolated state — so you can even use the same custom Hook twice in one component.

Custom Hooks are more of a convention than a feature. If a function’s name starts with ”use” and it calls other Hooks, we say it is a custom Hook. The useSomething naming convention is how our linter plugin is able to find bugs in the code using Hooks.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven’t considered. We are excited to see what custom Hooks the React community will come up with.

## useState

Functional replacement for `this.state` and `setState()`

```javascript
const [count, setCount] = useState(0);
const [color, setColor] = useState('black');
const [shape, setShape] = useState('circle');
```

However, unlike `this.setState` in a class, updating a state variable always replaces it instead of merging it.

## useEffect

Functional replacement for lifecycle methods syntax is:

```javascript
useEffect(() => {}, [])
```

useEffect Hooks let us split the code based on what it is doing rather than a lifecycle method name. React will apply every effect used by the component, in the order they were specified.

### componentDidMount optional use

Leave it empty.

This option is equal to a componentDidMount lifecycle method, meaning the hook runs one time when the component mounts (is inserted in the DOM tree)

```javascript
useEffect(() => {
  // Do something
}, []);
```

### componentDidUpdate optional use

Add a dependency to the array.

This way, the `useEffect` hook will re-run anytime the dependency, in this case `(color)` changes. This is similar to a `componentDidUpdate` method, with the only difference that it only runs when a certain condition has changed.

```javascript
useEffect(() => {
  // Do something
}, [color]);
```

If you use this optimization, make sure the array includes all values from the component scope (such as props and state) that change over time and that are used by the effect. Otherwise, your code will reference stale values from previous renders.

### componentDidMount and componentDidUpdate combo optional use

Leave out the dependency array.

You can also completely leave out the dependency array. This way, the useEffect hook runs anytime the component is updated, AND right after the initial render. This is the difference compared to the componentDidUpdate lifecycle method, because it also runs after the initial render. This way it would be equal to a componentDidMount and componentDidUpdate method combined.

```javascript
useEffect(() => {
  // Do something
});
```

### componentWillUnmount with return method

If you write a return statement like the above in a useEffect, it will do the same as a componentWillUnmount method.

```javascript
useEffect(() => {
  // Do something
}, [color]);
return () => {
  document.removeEventListener("click", changeColorOnClick);
};
```
