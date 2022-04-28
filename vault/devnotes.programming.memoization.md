---
id: vkst4fke381diy8f75f8rh4
title: Memoization
desc: 'Notes on Memoization'
updated: 1651164413519
created: 1650685441299
---
## Definition

In computing, memoization or memoisation is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again. Memoization has also been used in other contexts (and for purposes other than speed gains), such as in simple mutually recursive descent parsing. Although related to caching, memoization refers to a specific case of this optimization, distinguishing it from forms of caching such as buffering or page replacement. In the context of some logic programming languages, memoization is also known as tabling.

A memoized function "remembers" the results corresponding to some set of specific inputs. Subsequent calls with remembered inputs return the remembered result rather than recalculating it, thus eliminating the primary cost of a call with given parameters from all but the first call made to the function with those parameters. The set of remembered associations may be a fixed-size set controlled by a replacement algorithm or a fixed set, depending on the nature of the function and its use. A function can only be memoized if it is referentially transparent; that is, only if calling the function has exactly the same effect as replacing that function call with its return value. (Special case exceptions to this restriction exist, however.) While related to lookup tables, since memoization often uses such tables in its implementation, memoization populates its cache of results transparently on the fly, as needed, rather than in advance.

Memoization is a way to lower a function's time cost in exchange for space cost; that is, memoized functions become optimized for speed in exchange for a higher use of computer memory space. The time/space "cost" of algorithms has a specific name in computing: computational complexity. All functions have a computational complexity in time (i.e. they take time to execute) and in space.

Although a space–time tradeoff occurs (i.e., space used is speed gained), this differs from some other optimizations that involve time-space trade-off, such as strength reduction, in that memoization is a run-time rather than compile-time optimization. Moreover, strength reduction potentially replaces a costly operation such as multiplication with a less costly operation such as addition, and the results in savings can be highly machine-dependent (non-portable across machines), whereas memoization is a more machine-independent, cross-platform strategy.

### Example Memoization Function in JS

```javascript
// a simple pure function to get a value adding 10
const add = (n) => (n + 10);
console.log('Simple call', add(3));
// a simple memoize function that takes in a function
// and returns a memoized function
const memoize = (fn) => {
  let cache = {};
  return (...args) => {
    let n = args[0];  // just taking one argument here
    if (n in cache) {
      console.log('Fetching from cache');
      return cache[n];
    }
    else {
      console.log('Calculating result');
      let result = fn(n);
      cache[n] = result;
      return result;
    }
  }
}
// creating a memoized function for the 'add' pure function
const memoizedAdd = memoize(add);
console.log(memoizedAdd(3));  // calculated
console.log(memoizedAdd(3));  // cached
console.log(memoizedAdd(4));  // calculated
console.log(memoizedAdd(4));  // cached
```

### Is memoization same as caching?

Yes, kind of. Memoization is actually a specific type of caching. While caching can refer in general to any storing technique (like HTTP caching) for future use, memoizing specifically involves caching the return values of a function.

## Use Cases

- In order to memoize a function, it should be pure so that return values are the same for same inputs every time
- Memoizing is a trade-off between added space and added speed and thus only significant for functions having a limited input range so that cached values can be made use of more frequently
- It might look like you should memoize your API calls however it isn’t necessary because the browser automatically caches them for you. See HTTP caching for more detail
- The best use case I found for memoized functions is for heavy computational functions which can significantly improve performance (factorial and fibonacci are not really good real world examples)
- If you’re into React/Redux you can check out reselect which uses a memoized selector to ensure that calculations only happen when a change happens in a related part of the state tree.
