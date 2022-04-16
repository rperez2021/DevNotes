---
id: 7w5ugn5hasj4g83pm3pok6u
title: React
desc: 'Notes on ReactJS'
updated: 1650085966479
created: 1650074133094
---
## 3 Notes on Modern React Syntax

- We define variables with `let` and `const` statements. For the purposes of the React documentation, you can consider them equivalent to `var`.
- We use the `class` keyword to define JavaScript classes. There are two things worth remembering about them. Firstly, unlike with objects, you don't need to put commas between class method definitions. Secondly, unlike many other languages with classes, in JavaScript the value of this in a method depends on how it is called.
- We sometimes use `=>` to define "arrow functions". They're like regular functions, but shorter. For example, `x => x * 2` is roughly equivalent to `function(x) { return x * 2; }`. Importantly, arrow functions don't have their own this value so they're handy when you want to preserve the this value from an outer method definition.

## manifest.json

This is a web app manifest that describes your application, and it’s used by, e.g., mobile phones if a shortcut is added to the home screen.

Basically, the information read from this file is used to populate the web app’s icons, colors, names, etc.

## Functional vs Class Component

- Syntax is shorter for funtional
- Prior to React 16.8 (Hooks) you could not `setState()` in functional components
- Prior to React 16.8 (Hooks) you could not `useEffect` in functional components
- Functional Components are easier to read, create less code.

## Functional Components

- We don’t have to import and extend “Component” from React.
- We don’t need a constructor.
- We don’t need the render function, instead we put the return statement right at the end of the function body.

### 3 ways of defining and functional component

```jsx
import React from 'react';

function App() {
  return <div className="App">Hello World!</div>;
}

// OR (arrow-function syntax)

const App = () => {
  return <div className="App">Hello World!</div>;
};

// OR (implicit return)

const App = () => <div className="App">Hello World!</div>;

export default App;
```
