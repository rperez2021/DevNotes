---
id: 7w5ugn5hasj4g83pm3pok6u
title: React
desc: 'Notes on ReactJS'
updated: 1650170001877
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

## Props

Whether you declare a component as a function or a class it should be a pure function, it must never modify its own props.

**All React components must act like pure functions with respect to their props.**

### Destructuring Props in Components

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  constructor(props) {
    super(props);
  }

  render() {
    const { title, onButtonClicked } = this.props;

    return (
      <div>
        <h1>{title}</h1>
        <button onClick={onButtonClicked}>Click Me!</button>
      </div>
    );
  }
}

export default MyComponent;
```

### Binding This

Always remember: you must bind this for all methods in class components when passing them to other components.

```jsx
class App extends Component {
  constructor(props) {
    super(props);

    this.onClickBtn = this.onClickBtn.bind(this);
  }
```

## State

The following example of our simple counter app shows how to define state in React:

You **always** declare state in the constructor of a class component. Once again, this will work differently when we cover functional components later.

**IMPORTANT**: In React, state should be treated as **immutable**. This means you should never change state directly (i.e. without using `setState`) because it can lead to unexpected behavior or bugs.

In other words, you should never do something like: `this.state.count = 3`, or, `this.state.count++`. Instead, always use the `setState` method React provides to class components to modify the state.

```jsx
import React, { Component } from 'react';

class App extends Component {
  constructor() {
    super();

    this.state = {
      count: 0,
    };

    this.countUp = this.countUp.bind(this);
  }

  countUp() {
    this.setState({
      count: this.state.count + 1,
    });
  }

  render() {
    return (
      <div>
        <button onClick={this.countUp}>Click Me!</button>
        <p>{this.state.count}</p>
      </div>
    );
  }
}
```

### Using State Correctly

1. Do Not Modify State Directly

    ```jsx
    // Wrong
    this.state.comment = 'Hello';
    // Correct
    this.setState({comment: 'Hello'});
    ```

2. State Updates May Be Asynchronous

    React may batch multiple setState() calls into a single update for performance.

    Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

    ```jsx
    // Wrong
    this.setState({
        counter: this.state.counter + this.props.increment,
    });
    // Correct
    this.setState((state, props) => ({
        counter: state.counter + props.increment
    }));
    // Also works with a regular function
    this.setState(function(state, props) {
    return {
        counter: state.counter + props.increment
    };
    });
    ```

3. State Updates are Merged

    When you call `setState()`, React merges the object you provide into the current state.

    Your state may contain several independent variables that you can update them independently with separate `setState()` calls:

    ```jsx
        componentDidMount() {
        fetchPosts().then(response => {
        this.setState({
            posts: response.posts
        });
        });

        fetchComments().then(response => {
        this.setState({
            comments: response.comments
        });
        });
    }
    ```

### Data Flows Down

Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn’t care whether it is defined as a function or a class.

This is why state is often called local or encapsulated. It is not accessible to any component other than the one that owns and sets it.

A component may choose to pass its state down as props to its child components:

```jsx
<FormattedDate date={this.state.date} />
```

The `FormattedDate` component would receive the `date` in its props and wouldn’t know whether it came from the `Clock`’s state, from the `Clock`’s props, or was typed by hand.

This is commonly called a “top-down” or “unidirectional” data flow. Any state is always owned by some specific component, and any data or UI derived from that state can only affect components “below” them in the tree.

In React apps, whether a component is stateful or stateless is considered an implementation detail of the component that may change over time. You can use stateless components inside stateful components, and vice versa.