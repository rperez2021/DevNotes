---
id: nawckrkvlbw2c91aj4jj353
title: Higher Order Components - HOCS
desc: 'Notes on Higher Order Components'
updated: 1651105121615
created: 1651090334348
---
## General Info

A HOC is an advanced technique for reusing logic in React components. It is a pattern created out of React’s compositional nature.

HOCs basically incorporate the don’t-repeat-yourself (DRY) principle of programming, which you’ve most likely come across at some point in your career as a software developer. It is one of the best-known principles of software development, and observing it is very important when building an application or writing code in general.

Higher-order functions in JavaScript take some functions as arguments and return another function. They enable us to abstract over actions, not just values, They come in several forms, and they help us to write less code when operating on functions and even arrays.

### HOC Rules

1. We don’t modify or mutate components. We create new ones.
2. A HOC is used to compose components for code reuse.
3. A HOC is a pure function. It has no side effects, returning only a new component.

### Example Higher Order Function

```javascript
const formatCurrency = function( 
    currencySymbol,
    decimalSeparator  ) {
    return function( value ) {
        const wholePart = Math.trunc( value / 100 );
        let fractionalPart = value % 100;
        if ( fractionalPart < 10 ) {
            fractionalPart = '0' + fractionalPart;
        }
        return `${currencySymbol}${wholePart}${decimalSeparator}${fractionalPart}`;
    }
}
```

`formatCurrency` returns a function with a fixed currency symbol and decimal separator.

We then pass the formatter a value, and format this value with the function by extracting its whole part and the fractional part. The returned value of this function is constructed by a template literal, concatenating the currency symbol, the whole part, the decimal separator, and the fractional part.

Let’s use this higher-order function by assigning a value to it and seeing the result.

```shell
> getLabel = formatCurrency( '$', '.' );
 
> getLabel( 1999 )
"$19.99" //formatted value
 
> getLabel( 2499 )
"$24.99" //formatted value
```

### Example of a Higher Order Component

```javascript
import React from 'react';
// Take in a component as argument WrappedComponent
const higherOrderComponent = (WrappedComponent) => {
// And return another component
  class HOC extends React.Component {
    render() {
      return <WrappedComponent />;
    }
  }
  return HOC;
};
```

### Use Cases

- Show a loader while a component waits for data 
- Conditionally Rendered Components (different view for authed users)
- Components with Specific Styling (also by logged in or preference)
- Provide a component with a specific prop


