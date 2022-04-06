---
id: 0oq92n31j7l6xu624pphkih
title: Promises
desc: 'Notes on JS Promises'
updated: 1649007780427
created: 1649007780427
---
## General Info

Promises are a mechanism of handling asynchronous code, and they’re one you will see somewhat often when using other libraries or frameworks. Knowing what they are and how to use them is quite useful.

## From You Dont Know JS

Note: Because a Promise is externally immutable once resolved, it's now safe to pass that value around to any party and know that it cannot be modified accidentally or maliciously. This is especially true in relation to multiple parties observing the resolution of a Promise. It is not possible for one party to affect another party's ability to observe Promise resolution. Immutability may sound like an academic topic, but it's actually one of the most fundamental and important aspects of Promise design, and shouldn't be casually passed over.

The new Promise() constructor should only be used for legacy async tasks, like usage of `setTimeout` or `XMLHttpRequest`. A new Promise is created with the new keyword and the promise provides resolve and reject functions to the provided callback:

```javascript
var p = new Promise(function(resolve, reject) {
    // Do an async task async task and then...

    if(/* good condition */) {
        resolve('Success!');
    }
    else {
        reject('Failure!');
    }
});

p.then(function(result) { 
    /* do something with the result */
}).catch(function() {
    /* error :( */
}).finally(function() {
   /* executes regardless or success for failure */ 
});
```

It's up to the developer to manually call resolve or reject within the body of the callback based on the result of their given task. A realistic example would be converting XMLHttpRequest to a promise-based task:

```javascript
// From Jake Archibald's Promises and Back:
// http://www.html5rocks.com/en/tutorials/es6/promises/#toc-promisifying-xmlhttprequest

function get(url) {
  // Return a new promise.
  return new Promise(function(resolve, reject) {
    // Do the usual XHR stuff
    var req = new XMLHttpRequest();
    req.open('GET', url);

    req.onload = function() {
      // This is called even on 404 etc
      // so check the status
      if (req.status == 200) {
        // Resolve the promise with the response text
        resolve(req.response);
      }
      else {
        // Otherwise reject with the status text
        // which will hopefully be a meaningful error
        reject(Error(req.statusText));
      }
    };

    // Handle network errors
    req.onerror = function() {
      reject(Error("Network Error"));
    };

    // Make the request
    req.send();
  });
}

// Use it!
get('story.json').then(function(response) {
  console.log("Success!", response);
}, function(error) {
  console.error("Failed!", error);
});
```

Sometimes you don't need to complete an async tasks within the promise -- if it's possible that an async action will be taken, however, returning a promise will be best so that you can always count on a promise coming out of a given function. In that case you can simply call `Promise.resolve()` or `Promise.reject()` without using the new keyword. For example:

```javascript
var userCache = {};

function getUserDetail(username) {
  // In both cases, cached or not, a promise will be returned

  if (userCache[username]) {
    // Return a promise without the "new" keyword
    return Promise.resolve(userCache[username]);
  }

  // Use the fetch API to get the information
  // fetch returns a promise
  return fetch('users/' + username + '.json')
    .then(function(result) {
      userCache[username] = result;
      return result;
    })
    .catch(function() {
      throw new Error('Could not find user: ' + username);
    });
}
```

### then()

All promise instances get a then method which allows you to react to the promise.  The first then method callback receives the result given to it by the resolve() call:

```javascript
new Promise(function(resolve, reject) {
    // A mock async action using setTimeout
    setTimeout(function() { resolve(10); }, 3000);
})
.then(function(result) {
    console.log(result);
});

// From the console:
// 10
```

The then callback is triggered when the promise is resolved.  You can also chain then method callbacks:

```javascript
new Promise(function(resolve, reject) { 
    // A mock async action using setTimeout
    setTimeout(function() { resolve(10); }, 3000);
})
.then(function(num) { console.log('first then: ', num); return num * 2; })
.then(function(num) { console.log('second then: ', num); return num * 2; })
.then(function(num) { console.log('last then: ', num);});

// From the console:
// first then:  10
// second then:  20
// last then:  40
```

### catch()

The catch callback is executed when the promise is rejected:

```javascript
new Promise(function(resolve, reject) {
    // A mock async action using setTimeout
    setTimeout(function() { reject('Done!'); }, 3000);
})
.then(function(e) { console.log('done', e); })
.catch(function(e) { console.log('catch: ', e); });

// From the console:
// 'catch: Done!'
```

### finally()

The newly introduced finally callback is called regardless of success or failure:

```javascript
(new Promise((resolve, reject) => { reject("Nope"); }))
    .then(() => { console.log("success") })
    .catch(() => { console.log("fail") })
    .finally(res => { console.log("finally") });

// >> fail
// >> finally
```

### Promise.all

Think about JavaScript loaders:  there are times when you trigger multiple async interactions but only want to respond when all of them are completed -- that's where Promise.all comes in.  The Promise.all method takes an array of promises and fires one callback once they are all resolved:

```javascript
Promise.all([promise1, promise2]).then(function(results) {
    // Both promises resolved
})
.catch(function(error) {
    // One or more promises was rejected
});
```

A perfect way of thinking about Promise.all is firing off multiple AJAX (via fetch) requests at one time:

```javascript
var request1 = fetch('/users.json');
var request2 = fetch('/articles.json');

Promise.all([request1, request2]).then(function(results) {
    // Both promises done!
});
```

You could combine APIs like fetch and the Battery API since they both return promises:

```javascript
Promise.all([fetch('/users.json'), navigator.getBattery()]).then(function(results) {
    // Both promises done!
});
```

Dealing with rejection is, of course, hard. If any promise is rejected the catch fires for the first rejection:

```javascript
var req1 = new Promise(function(resolve, reject) { 
    // A mock async action using setTimeout
    setTimeout(function() { resolve('First!'); }, 4000);
});
var req2 = new Promise(function(resolve, reject) { 
    // A mock async action using setTimeout
    setTimeout(function() { reject('Second!'); }, 3000);
});
Promise.all([req1, req2]).then(function(results) {
    console.log('Then: ', results);
}).catch(function(err) {
    console.log('Catch: ', err);
});

// From the console:
// Catch: Second!
```

### Promise.race()

Promise.race is an interesting function -- instead of waiting for all promises to be resolved or rejected, Promise.race triggers as soon as any promise in the array is resolved or rejected:

```javascript
var req1 = new Promise(function(resolve, reject) { 
    // A mock async action using setTimeout
    setTimeout(function() { resolve('First!'); }, 8000);
});
var req2 = new Promise(function(resolve, reject) { 
    // A mock async action using setTimeout
    setTimeout(function() { resolve('Second!'); }, 3000);
});
Promise.race([req1, req2]).then(function(one) {
    console.log('Then: ', one);
}).catch(function(one, two) {
    console.log('Catch: ', one);
});

// From the console:
// Then: Second!
```

A use case could be triggering a request to a primary source and a secondary source (in case the primary or secondary are unavailable).

### Completion Event

Whether you call it a "completion event" or a "continuation event" depends on your perspective. Is the focus more on what happens with foo(..), or what happens after `foo(..)` finishes? Both perspectives are accurate and useful. The event notification tells us that `foo(..)` has completed, but also that it's OK to continue with the next step. Indeed, the callback you pass to be called for the event notification is itself what we've previously called a continuation. Because completion event is a bit more focused on the foo(..), which more has our attention at present, we slightly favor completion event for the rest of this text.

The pattern shown with `new Promise( function(..){ .. } )` is generally called the "revealing constructor". The function passed in is executed immediately (not async deferred, as callbacks to then(..) are), and it's provided two parameters, which in this case we've named resolve and reject. These are the resolution functions for the promise. resolve(..) generally signals fulfillment, and `reject(..)` signals rejection.

### Thenable Duck Typing

An important detail is how to know for sure if some value is a genuine Promise or not. Or more directly, is it a value that will behave like a Promise?

Given that Promises are constructed by the new Promise(..) syntax, you might think that p instanceof Promise would be an acceptable check. But unfortunately, there are a number of reasons that's not totally sufficient.

Mainly, you can receive a Promise value from another browser window (iframe, etc.), which would have its own Promise different from the one in the current window/frame, and that check would fail to identify the Promise instance.

As such, it was decided that the way to recognize a Promise (or something that behaves like a Promise) would be to define something called a "thenable" as any object or function which has a then(..) method on it. It is assumed that any such value is a Promise-conforming thenable.

The standards decision to hijack the previously nonreserved -- and completely general-purpose sounding -- then property name means that no value (or any of its delegates), either past, present, or future, can have a then(..) function present, either on purpose or by accident, or that value will be confused for a thenable in Promises systems, which will probably create bugs that are really hard to track down.

*Warning*: I do not like how we ended up with duck typing of thenables for Promise recognition. There were other options, such as "branding" or even "anti-branding"; what we got seems like a worst-case compromise. But it's not all doom and gloom. Thenable duck typing can be helpful, as we'll see later. Just beware that thenable duck typing can be hazardous if it incorrectly identifies something as a Promise that isn't.

### Promise Trust

Whereas the future values and completion events analogies play out explicitly in the code patterns we've explored, it won't be entirely obvious why or how Promises are designed to solve all of the inversion of control trust issues we laid out in the "Trust Issues" section of Chapter 2. But with a little digging, we can uncover some important guarantees that restore the confidence in async coding that Chapter 2 tore down!

Let's start by reviewing the trust issues with callbacks-only coding. When you pass a callback to a utility foo(..), it might:

- Call the callback too early
- Call the callback too late (or never)
- Call the callback too few or too many times
- Fail to pass along any necessary environment/parameters
- Swallow any errors/exceptions that may happen

The characteristics of Promises are intentionally designed to provide useful, repeatable answers to all these concerns.

#### Calling Too Early

Primarily, this is a concern of whether code can introduce Zalgo-like effects (see Chapter 2), where sometimes a task finishes synchronously and sometimes asynchronously, which can lead to race conditions.

Promises by definition cannot be susceptible to this concern, because even an immediately fulfilled Promise (like new Promise(function(resolve){ resolve(42); })) cannot be observed synchronously.

That is, when you call then(..) on a Promise, even if that Promise was already resolved, the callback you provide to then(..) will always be called asynchronously (for more on this, refer back to "Jobs" in Chapter 1).

No more need to insert your own setTimeout(..,0) hacks. Promises prevent Zalgo automatically.

#### Calling Too Late

Similar to the previous point, a Promise's then(..) registered observation callbacks are automatically scheduled when either resolve(..) or reject(..) are called by the Promise creation capability. Those scheduled callbacks will predictably be fired at the next asynchronous moment (see "Jobs" in Chapter 1).

It's not possible for synchronous observation, so it's not possible for a synchronous chain of tasks to run in such a way to in effect "delay" another callback from happening as expected. That is, when a Promise is resolved, all then(..) registered callbacks on it will be called, in order, immediately at the next asynchronous opportunity (again, see "Jobs" in Chapter 1), and nothing that happens inside of one of those callbacks can affect/delay the calling of the other callbacks.

#### Promise Scheduling Quirks

It's important to note, though, that there are lots of nuances of scheduling where the relative ordering between callbacks chained off two separate Promises is not reliably predictable.

If two promises p1 and p2 are both already resolved, it should be true that p1.then(..); p2.then(..) would end up calling the callback(s) for p1 before the ones for p2. But there are subtle cases where that might not be true, such as the following:

```javascript
var p3 = new Promise( function(resolve,reject){
  resolve( "B" );
} );

var p1 = new Promise( function(resolve,reject){
  resolve( p3 );
} );

var p2 = new Promise( function(resolve,reject){
  resolve( "A" );
} );

p1.then( function(v){
  console.log( v );
} );

p2.then( function(v){
  console.log( v );
} );

// A B  <-- not  B A  as you might expect
```

We'll cover this more later, but as you can see, p1 is resolved not with an immediate value, but with another promise p3 which is itself resolved with the value "B". The specified behavior is to unwrap p3 into p1, but asynchronously, so p1's callback(s) are behind p2's callback(s) in the asynchronous Job queue

To avoid such nuanced nightmares, you should never rely on anything about the ordering/scheduling of callbacks across Promises. In fact, a good practice is not to code in such a way where the ordering of multiple callbacks matters at all. Avoid that if you can.

#### Never Calling the Callback

This is a very common concern. It's addressable in several ways with Promises.

First, nothing (not even a JS error) can prevent a Promise from notifying you of its resolution (if it's resolved). If you register both fulfillment and rejection callbacks for a Promise, and the Promise gets resolved, one of the two callbacks will always be called.

Of course, if your callbacks themselves have JS errors, you may not see the outcome you expect, but the callback will in fact have been called. We'll cover later how to be notified of an error in your callback, because even those don't get swallowed.

But what if the Promise itself never gets resolved either way? Even that is a condition that Promises provide an answer for, using a higher level abstraction called a "race":

```javascript
// a utility for timing out a Promise
function timeoutPromise(delay) {
  return new Promise( function(resolve,reject){
    setTimeout( function(){
      reject( "Timeout!" );
    }, delay );
  } );
}

// setup a timeout for `foo()`
Promise.race( [
  foo(),  // attempt `foo()`
  timeoutPromise( 3000 )  // give it 3 seconds
] )
.then(
  function(){
    // `foo(..)` fulfilled in time!
  },
  function(err){
    // either `foo()` rejected, or it just
    // didn't finish in time, so inspect
    // `err` to know which
  }
);
```

There are more details to consider with this Promise timeout pattern, but we'll come back to it later.

Importantly, we can ensure a signal as to the outcome of foo(), to prevent it from hanging our program indefinitely.

#### Calling Too Few or Too Many Times

By definition, one is the appropriate number of times for the callback to be called. The "too few" case would be zero calls, which is the same as the "never" case we just examined.

The "too many" case is easy to explain. Promises are defined so that they can only be resolved once. If for some reason the Promise creation code tries to call resolve(..) or reject(..) multiple times, or tries to call both, the Promise will accept only the first resolution, and will silently ignore any subsequent attempts.

Because a Promise can only be resolved once, any then(..) registered callbacks will only ever be called once (each).

Of course, if you register the same callback more than once, (e.g., p.then(f); p.then(f);), it'll be called as many times as it was registered. The guarantee that a response function is called only once does not prevent you from shooting yourself in the foot.

#### Failing to Pass Along Any Parameters/Environment

Promises can have, at most, one resolution value (fulfillment or rejection).

If you don't explicitly resolve with a value either way, the value is undefined, as is typical in JS. But whatever the value, it will always be passed to all registered (and appropriate: fulfillment or rejection) callbacks, either now or in the future.

Something to be aware of: If you call `resolve(..)` or `reject(..)` with multiple parameters, all subsequent parameters beyond the first will be silently ignored. Although that might seem a violation of the guarantee we just described, it's not exactly, because it constitutes an invalid usage of the Promise mechanism. Other invalid usages of the API (such as calling `resolve(..)` multiple times) are similarly protected, so the Promise behavior here is consistent (if not a tiny bit frustrating).

If you want to pass along multiple values, you must wrap them in another single value that you pass, such as an array or an object.

As for environment, functions in JS always retain their closure of the scope in which they're defined (see the Scope & Closures title of this series), so they of course would continue to have access to whatever surrounding state you provide. Of course, the same is true of callbacks-only design, so this isn't a specific augmentation of benefit from Promises -- but it's a guarantee we can rely on nonetheless.

#### Swallowing Any Errors/Exceptions

In the base sense, this is a restatement of the previous point. If you reject a Promise with a reason (aka error message), that value is passed to the rejection callback(s).

But there's something much bigger at play here. If at any point in the creation of a Promise, or in the observation of its resolution, a JS exception error occurs, such as a TypeError or ReferenceError, that exception will be caught, and it will force the Promise in question to become rejected.

For example:

```javascript
var p = new Promise( function(resolve,reject){
  foo.bar();  // `foo` is not defined, so error!
  resolve( 42 );  // never gets here :(
} );

p.then(
  function fulfilled(){
    // never gets here :(
  },
  function rejected(err){
    // `err` will be a `TypeError` exception object
    // from the `foo.bar()` line.
  }
);
```

The JS exception that occurs from `foo.bar()` becomes a Promise rejection that you can catch and respond to.

This is an important detail, because it effectively solves another potential Zalgo moment, which is that errors could create a synchronous reaction whereas nonerrors would be asynchronous. Promises turn even JS exceptions into asynchronous behavior, thereby reducing the race condition chances greatly.

But what happens if a Promise is fulfilled, but there's a JS exception error during the observation (in a `then(..)` registered callback)? Even those aren't lost, but you may find how they're handled a bit surprising, until you dig in a little deeper:

```javascript
var p = new Promise( function(resolve,reject){
  resolve( 42 );
} );

p.then(
  function fulfilled(msg){
    foo.bar();
    console.log( msg ); // never gets here :(
  },
  function rejected(err){
    // never gets here either :(
  }
);
```

Wait, that makes it seem like the exception from `foo.bar()` really did get swallowed. Never fear, it didn't. But something deeper is wrong, which is that we've failed to listen for it. The `p.then(..)` call itself returns another promise, and it's that promise that will be rejected with the TypeError exception.

Why couldn't it just call the error handler we have defined there? Seems like a logical behavior on the surface. **But it would violate the fundamental principle that Promises are immutable once resolved. p was already fulfilled to the value 42, so it can't later be changed to a rejection just because there's an error in observing p's resolution.**

Besides the principle violation, such behavior could wreak havoc, if say there were multiple `then(..)` registered callbacks on the promise p, because some would get called and others wouldn't, and it would be very opaque as to why.

#### Trustable Promise?

There's one last detail to examine to establish trust based on the Promise pattern.

You've no doubt noticed that Promises don't get rid of callbacks at all. They just change where the callback is passed to. Instead of passing a callback to `foo(..)`, we get something (ostensibly a genuine Promise) back from `foo(..)`, and we pass the callback to that something instead.

But why would this be any more trustable than just callbacks alone? How can we be sure the something we get back is in fact a trustable Promise? Isn't it basically all just a house of cards where we can trust only because we already trusted?

One of the most important, but often overlooked, details of Promises is that they have a solution to this issue as well. Included with the native ES6 Promise implementation is `Promise.resolve(..)`.

If you pass an immediate, non-Promise, non-thenable value to `Promise.resolve(..)`, you get a promise that's fulfilled with that value. In other words, these two promises p1 and p2 will behave basically identically:

```javascript
var p1 = new Promise( function(resolve,reject){
  resolve( 42 );
} );

var p2 = Promise.resolve( 42 );
```

But if you pass a genuine Promise to `Promise.resolve(..)`, you just get the same promise back:

```javascript
var p1 = Promise.resolve( 42 );

var p2 = Promise.resolve( p1 );

p1 === p2; // true
```

Even more importantly, if you pass a non-Promise thenable value to `Promise.resolve(..)`, it will attempt to unwrap that value, and the unwrapping will keep going until a concrete final non-Promise-like value is extracted.

Recall our previous discussion of thenables?

Consider:

```javascript
var p = {
  then: function(cb) {
    cb( 42 );
  }
};

// this works OK, but only by good fortune
p
.then(
  function fulfilled(val){
    console.log( val ); // 42
  },
  function rejected(err){
    // never gets here
  }
);
```

This p is a thenable, but it's not a genuine Promise. Luckily, it's reasonable, as most will be. But what if you got back instead something that looked like:

```javascript
var p = {
  then: function(cb,errcb) {
    cb( 42 );
    errcb( "evil laugh" );
  }
};

p
.then(
  function fulfilled(val){
    console.log( val ); // 42
  },
  function rejected(err){
    // oops, shouldn't have run
    console.log( err ); // evil laugh
  }
);
```

This p is a thenable but it's not so well behaved of a promise. Is it malicious? Or is it just ignorant of how Promises should work? It doesn't really matter, to be honest. In either case, it's not trustable as is.

Nonetheless, we can pass either of these versions of p to `Promise.resolve(..)`, and we'll get the normalized, safe result we'd expect:

```javascript
Promise.resolve( p )
.then(
  function fulfilled(val){
    console.log( val ); // 42
  },
  function rejected(err){
    // never gets here
  }
);
```

`Promise.resolve(..)` will accept any thenable, and will unwrap it to its non-thenable value. But you get back from `Promise.resolve(..)` a real, genuine Promise in its place, one that you can trust. If what you passed in is already a genuine Promise, you just get it right back, so there's no downside at all to filtering through `Promise.resolve(..)` to gain trust.

So let's say we're calling a `foo(..)` utility and we're not sure we can trust its return value to be a well-behaving Promise, but we know it's at least a thenable. `Promise.resolve(..)` will give us a trustable Promise wrapper to chain off of:

```javascript
// don't just do this:
foo( 42 )
.then( function(v){
  console.log( v );
} );

// instead, do this:
Promise.resolve( foo( 42 ) )
.then( function(v){
  console.log( v );
} );
```

Note: Another beneficial side effect of wrapping `Promise.resolve(..)` around any function's return value (thenable or not) is that it's an easy way to normalize that function call into a well-behaving async task. If `foo(42)` returns an immediate value sometimes, or a Promise other times, `Promise.resolve( foo(42) )` makes sure it's always a Promise result. And avoiding Zalgo makes for much better code.

### Chain Flow

We've hinted at this a couple of times already, but Promises are not just a mechanism for a single-step this-then-that sort of operation. That's the building block, of course, but it turns out we can string multiple Promises together to represent a sequence of async steps.

The key to making this work is built on two behaviors intrinsic to Promises:

- Every time you call `then(..)` on a Promise, it creates and returns a new Promise, which we can chain with.
- Whatever value you return from the `then(..)` call's fulfillment callback (the first parameter) is automatically set as the fulfillment of the chained Promise (from the first point).

Let's first illustrate what that means, and then we'll derive how that helps us create async sequences of flow control. Consider the following:

```javascript
var p = Promise.resolve( 21 );

var p2 = p.then( function(v){
  console.log( v ); // 21

  // fulfill `p2` with value `42`
  return v * 2;
} );

// chain off `p2`
p2.then( function(v){
  console.log( v ); // 42
} );
```

By returning `v * 2 (i.e., 42)`, we fulfill the p2 promise that the first `then(..)` call created and returned. When p2's `then(..)` call runs, it's receiving the fulfillment from the return `v * 2` statement. Of course, p2.`then(..)` creates yet another promise, which we could have stored in a p3 variable.

But it's a little annoying to have to create an intermediate variable p2 (or p3, etc.). Thankfully, we can easily just chain these together:

```javascript
var p = Promise.resolve( 21 );

p
.then( function(v){
  console.log( v ); // 21

  // fulfill the chained promise with value `42`
  return v * 2;
} )
// here's the chained promise
.then( function(v){
  console.log( v ); // 42
} );
```

So now the first `then(..)` is the first step in an async sequence, and the second `then(..)` is the second step. This could keep going for as long as you needed it to extend. Just keep chaining off a previous `then(..)` with each automatically created Promise.

But there's something missing here. What if we want step 2 to wait for step 1 to do something asynchronous? We're using an immediate return statement, which immediately fulfills the chained promise.

The key to making a Promise sequence truly async capable at every step is to recall how `Promise.resolve(..)` operates when what you pass to it is a Promise or thenable instead of a final value. `Promise.resolve(..)` directly returns a received genuine Promise, or it unwraps the value of a received thenable -- and keeps going recursively while it keeps unwrapping thenables.

The same sort of unwrapping happens if you return a thenable or Promise from the fulfillment (or rejection) handler. Consider:

```javascript
var p = Promise.resolve( 21 );

p.then( function(v){
  console.log( v ); // 21

  // create a promise and return it
  return new Promise( function(resolve,reject){
    // fulfill with value `42`
    resolve( v * 2 );
  } );
} )
.then( function(v){
  console.log( v ); // 42
} );
```

Even though we wrapped 42 up in a promise that we returned, it still got unwrapped and ended up as the resolution of the chained promise, such that the second `then(..)` still received 42. If we introduce asynchrony to that wrapping promise, everything still nicely works the same:

```javascript
var p = Promise.resolve( 21 );

p.then( function(v){
  console.log( v ); // 21

  // create a promise to return
  return new Promise( function(resolve,reject){
    // introduce asynchrony!
    setTimeout( function(){
      // fulfill with value `42`
      resolve( v * 2 );
    }, 100 );
  } );
} )
.then( function(v){
  // runs after the 100ms delay in the previous step
  console.log( v ); // 42
} );
```

That's incredibly powerful! Now we can construct a sequence of however many async steps we want, and each step can delay the next step (or not!), as necessary.

Of course, the value passing from step to step in these examples is optional. If you don't return an explicit value, an implicit undefined is assumed, and the promises still chain together the same way. **Each Promise resolution is thus just a signal to proceed to the next step.**

To further the chain illustration, let's generalize a delay-Promise creation (without resolution messages) into a utility we can reuse for multiple steps:

```javascript
function delay(time) {
  return new Promise( function(resolve,reject){
    setTimeout( resolve, time );
  } );
}

delay( 100 ) // step 1
.then( function STEP2(){
  console.log( "step 2 (after 100ms)" );
  return delay( 200 );
} )
.then( function STEP3(){
  console.log( "step 3 (after another 200ms)" );
} )
.then( function STEP4(){
  console.log( "step 4 (next Job)" );
  return delay( 50 );
} )
.then( function STEP5(){
  console.log( "step 5 (after another 50ms)" );
} )
```

...
Calling delay(200) creates a promise that will fulfill in 200ms, and then we return that from the first then(..) fulfillment callback, which causes the second then(..)'s promise to wait on that 200ms promise.

Note: As described, technically there are two promises in that interchange: the 200ms-delay promise and the chained promise that the second `then(..)` chains from. But you may find it easier to mentally combine these two promises together, because the Promise mechanism automatically merges their states for you. In that respect, you could think of return delay(200) as creating a promise that replaces the earlier-returned chained promise.

To be honest, though, sequences of delays with no message passing isn't a terribly useful example of Promise flow control. Let's look at a scenario that's a little more practical.

Instead of timers, let's consider making Ajax requests:

```javascript
// assume an `ajax( {url}, {callback} )` utility

// Promise-aware ajax
function request(url) {
  return new Promise( function(resolve,reject){
  // the `ajax(..)` callback should be our
  // promise's `resolve(..)` function
    ajax( url, resolve );
  } );
}
```

We first define a `request(..)` utility that constructs a promise to represent the completion of the `ajax(..)` call:

```javascript
request( "http://some.url.1/" )
.then( function(response1){
  return request( "http://some.url.2/?v=" + response1 );
} )
.then( function(response2){
  console.log( response2 );
} );
```

Note: Developers commonly encounter situations in which they want to do Promise-aware async flow control with utilities that are not themselves Promise-enabled (like `ajax(..)` here, which expects a callback). Although the native ES6 Promise mechanism doesn't automatically solve this pattern for us, practically all Promise libraries do. They usually call this process "lifting" or "promisifying" or some variation thereof. We'll come back to this technique later.

Using the Promise-returning `request(..)`, we create the first step in our chain implicitly by calling it with the first URL, and chain off that returned promise with the first `then(..)`.

Once response1 comes back, we use that value to construct a second URL, and make a second request(..) call. That second `request(..)` promise is returned so that the third step in our async flow control waits for that Ajax call to complete. Finally, we print response2 once it returns.

The Promise chain we construct is not only a flow control that expresses a multistep async sequence, but it also acts as a message channel to propagate messages from step to step.

What if something went wrong in one of the steps of the Promise chain? An error/exception is on a per-Promise basis, which means it's possible to catch such an error at any point in the chain, and that catching acts to sort of "reset" the chain back to normal operation at that point:

```javascript
// step 1:
request( "http://some.url.1/" )

// step 2:
.then( function(response1){
 foo.bar(); // undefined, error!

 // never gets here
 return request( "http://some.url.2/?v=" + response1 );
} )

// step 3:
.then(
 function fulfilled(response2){
  // never gets here
  },
  // rejection handler to catch the error
  function rejected(err){
    console.log( err ); // `TypeError` from `foo.bar()` error
    return 42;
  }
)

// step 4:
.then( function(msg){
  console.log( msg );   // 42
} );
```

When the error occurs in step 2, the rejection handler in step 3 catches it. The return value (42 in this snippet), if any, from that rejection handler fulfills the promise for the next step (4), such that the chain is now back in a fulfillment state.

Note: As we discussed earlier, when returning a promise from a fulfillment handler, it's unwrapped and can delay the next step. That's also true for returning promises from rejection handlers, such that if the `return 42` in step 3 instead returned a promise, that promise could delay step 4. A thrown exception inside either the fulfillment or rejection handler of a `then(..)` call causes the next (chained) promise to be immediately rejected with that exception.

If you call `then(..)` on a promise, and you only pass a fulfillment handler to it, an assumed rejection handler is substituted:

```javascript
var p = new Promise( function(resolve,reject){
  reject( "Oops" );
} );

var p2 = p.then(
  function fulfilled(){
    // never gets here
  }
  // assumed rejection handler, if omitted or
  // any other non-function value passed
  // function(err) {
  //     throw err;
  // }
);
```

As you can see, the assumed rejection handler simply rethrows the error, which ends up forcing p2 (the chained promise) to reject with the same error reason. In essence, this allows the error to continue propagating along a Promise chain until an explicitly defined rejection handler is encountered.

Note: We'll cover more details of error handling with Promises a little later, because there are other nuanced details to be concerned about.

If a proper valid function is not passed as the fulfillment handler parameter to `then(..)`, there's also a default handler substituted:

```javascript
var p = Promise.resolve( 42 );

p.then(
  // assumed fulfillment handler, if omitted or
  // any other non-function value passed
  // function(v) {
  //     return v;
  // }
  null,
  function rejected(err){
    // never gets here
  }
);
```

As you can see, the default fulfillment handler simply passes whatever value it receives along to the next step (Promise).

Note: The `then(null,function(err){ .. })` pattern -- only handling rejections (if any) but letting fulfillments pass through -- has a shortcut in the API: `catch(function(err){ .. })`. We'll cover `catch(..)` more fully in the next section.

Let's review briefly the intrinsic behaviors of Promises that enable chaining flow control:

A `then(..)` call against one Promise automatically produces a new Promise to return from the call.
Inside the fulfillment/rejection handlers, if you return a value or an exception is thrown, the new returned (chainable) Promise is resolved accordingly.
If the fulfillment or rejection handler returns a Promise, it is unwrapped, so that whatever its resolution is will become the resolution of the chained Promise returned from the current `then(..)`.
While chaining flow control is helpful, it's probably most accurate to think of it as a side benefit of how Promises compose (combine) together, rather than the main intent. As we've discussed in detail several times already, Promises normalize asynchrony and encapsulate time-dependent value state, and that is what lets us chain them together in this useful way.

Certainly, the sequential expressiveness of the chain (this-then-this-then-this...) is a big improvement over the tangled mess of callbacks as we identified in Chapter 2. But there's still a fair amount of boilerplate `(then(..) and function(){ .. })` to wade through. In the next chapter, we'll see a significantly nicer pattern for sequential flow control expressivity, with generators.

### Error Handling

We've already seen several examples of how Promise rejection -- either intentional through calling `reject(..)` or accidental through JS exceptions -- allows saner error handling in asynchronous programming. Let's circle back though and be explicit about some of the details that we glossed over.

The most natural form of error handling for most developers is the synchronous `try..catch` construct. Unfortunately, it's synchronous-only, so it fails to help in async code patterns:

```javascript
function foo() {
  setTimeout( function(){
    baz.bar();
  }, 100 );
}

try {
  foo();
  // later throws global error from `baz.bar()`
}
catch (err) {
  // never gets here
}
```

`try..catch` would certainly be nice to have, but it doesn't work across async operations. That is, unless there's some additional environmental support, which we'll come back to with generators in Chapter 4.

In callbacks, some standards have emerged for patterned error handling, most notably the "error-first callback" style:

```javascript
function foo(cb) {
  setTimeout( function(){
    try {
      var x = baz.bar();
      cb( null, x ); // success!
    }
    catch (err) {
      cb( err );
    }
  }, 100 );
}

foo( function(err,val){
  if (err) {
    console.error( err ); // bummer :(
  }
  else {
    console.log( val );
  }
} );
```

Note: The `try..catch` here works only from the perspective that the `baz.bar()` call will either succeed or fail immediately, synchronously. If `baz.bar()` was itself its own async completing function, any async errors inside it would not be catchable.

The callback we pass to `foo(..)` expects to receive a signal of an error by the reserved first parameter err. If present, error is assumed. If not, success is assumed.

This sort of error handling is technically async capable, but it doesn't compose well at all. Multiple levels of error-first callbacks woven together with these ubiquitous if statement checks inevitably will lead you to the perils of callback hell (see Chapter 2).

So we come back to error handling in Promises, with the rejection handler passed to `then(..)`. Promises don't use the popular "error-first callback" design style, but instead use "split callbacks" style; there's one callback for fulfillment and one for rejection:

```javascript
var p = Promise.reject( "Oops" );

p.then(
  function fulfilled(){
    // never gets here
  },
  function rejected(err){
    console.log( err ); // "Oops"
  }
);
```

While this pattern of error handling makes fine sense on the surface, the nuances of Promise error handling are often a fair bit more difficult to fully grasp.

Consider:

```javascript
var p = Promise.resolve( 42 );

p.then(
  function fulfilled(msg){
    // numbers don't have string functions,
    // so will throw an error
    console.log( msg.toLowerCase() );
  },
  function rejected(err){
    // never gets here
  }
);
```

If the `msg.toLowerCase()` legitimately throws an error (it does!), why doesn't our error handler get notified? As we explained earlier, it's because that error handler is for the p promise, which has already been fulfilled with value 42. The p promise is immutable, so the only promise that can be notified of the error is the one returned from `p.then(..)`, which in this case we don't capture.

That should paint a clear picture of why error handling with Promises is error-prone (pun intended). It's far too easy to have errors swallowed, as this is very rarely what you'd intend.

Warning: If you use the Promise API in an invalid way and an error occurs that prevents proper Promise construction, the result will be an immediately thrown exception, not a rejected Promise. Some examples of incorrect usage that fail Promise construction: `new Promise(null)`, `Promise.all()`, `Promise.race(42)`, and so on. You can't get a rejected Promise if you don't use the Promise API validly enough to actually construct a Promise in the first place!

#### Pit of Despair

Jeff Atwood noted years ago: programming languages are often set up in such a way that by default, developers fall into the [pit of despair](http://blog.codinghorror.com/falling-into-the-pit-of-success/) -- where accidents are punished -- and that you have to try harder to get it right. He implored us to instead create a "pit of success," where by default you fall into expected (successful) action, and thus would have to try hard to fail.

Promise error handling is unquestionably "pit of despair" design. By default, it assumes that you want any error to be swallowed by the Promise state, and if you forget to observe that state, the error silently languishes/dies in obscurity -- usually despair.

To avoid losing an error to the silence of a forgotten/discarded Promise, some developers have claimed that a "best practice" for Promise chains is to always end your chain with a final catch(..), like:

```javascript
var p = Promise.resolve( 42 );

p.then(
  function fulfilled(msg){
    // numbers don't have string functions,
    // so will throw an error
    console.log( msg.toLowerCase() );
  }
)
.catch( handleErrors );
```

Because we didn't pass a rejection handler to the then(..), the default handler was substituted, which simply propagates the error to the next promise in the chain. As such, both errors that come into p, and errors that come after p in its resolution (like the msg.toLowerCase() one) will filter down to the final handleErrors(..).

Problem solved, right? Not so fast!

What happens if `handleErrors(..)` itself also has an error in it? Who catches that? There's still yet another unattended promise: the one `catch(..)` returns, which we don't capture and don't register a rejection handler for.

You can't just stick another catch(..) on the end of that chain, because it too could fail. The last step in any Promise chain, whatever it is, always has the possibility, even decreasingly so, of dangling with an uncaught error stuck inside an unobserved Promise.

Sound like an impossible conundrum yet?

#### Uncaught Handling

It's not exactly an easy problem to solve completely. There are other ways to approach it which many would say are better.

Some Promise libraries have added methods for registering something like a "global unhandled rejection" handler, which would be called instead of a globally thrown error. But their solution for how to identify an error as "uncaught" is to have an arbitrary-length timer, say 3 seconds, running from time of rejection. If a Promise is rejected but no error handler is registered before the timer fires, then it's assumed that you won't ever be registering a handler, so it's "uncaught."

In practice, this has worked well for many libraries, as most usage patterns don't typically call for significant delay between Promise rejection and observation of that rejection. But this pattern is troublesome because 3 seconds is so arbitrary (even if empirical), and also because there are indeed some cases where you want a Promise to hold on to its rejectedness for some indefinite period of time, and you don't really want to have your "uncaught" handler called for all those false positives (not-yet-handled "uncaught errors").

Another more common suggestion is that Promises should have a `done(..)` added to them, which essentially marks the Promise chain as "done." `done(..)` doesn't create and return a Promise, so the callbacks passed to `done(..)` are obviously not wired up to report problems to a chained Promise that doesn't exist.

So what happens instead? It's treated as you might usually expect in uncaught error conditions: any exception inside a `done(..)` rejection handler would be thrown as a global uncaught error (in the developer console, basically):

```javascript
var p = Promise.resolve( 42 );

p.then(
  function fulfilled(msg){
    // numbers don't have string functions,
    // so will throw an error
    console.log( msg.toLowerCase() );
  }
)
.done( null, handleErrors );

// if `handleErrors(..)` caused its own exception, it would
// be thrown globally here
```

This might sound more attractive than the never-ending chain or the arbitrary timeouts. But the biggest problem is that it's not part of the ES6 standard, so no matter how good it sounds, at best it's a lot longer way off from being a reliable and ubiquitous solution.

Are we just stuck, then? Not entirely.

Browsers have a unique capability that our code does not have: they can track and know for sure when any object gets thrown away and garbage collected. So, browsers can track Promise objects, and whenever they get garbage collected, if they have a rejection in them, the browser knows for sure this was a legitimate "uncaught error," and can thus confidently know it should report it to the developer console.

Note: At the time of this writing, both Chrome and Firefox have early attempts at that sort of "uncaught rejection" capability, though support is incomplete at best.

However, if a Promise doesn't get garbage collected -- it's exceedingly easy for that to accidentally happen through lots of different coding patterns -- the browser's garbage collection sniffing won't help you know and diagnose that you have a silently rejected Promise laying around.

Is there any other alternative? Yes.

#### Pit of Success

The following is just theoretical, how Promises could be someday changed to behave. I believe it would be far superior to what we currently have. And I think this change would be possible even post-ES6 because I don't think it would break web compatibility with ES6 Promises. Moreover, it can be polyfilled/prollyfilled in, if you're careful. Let's take a look:

Promises could default to reporting (to the developer console) any rejection, on the next Job or event loop tick, if at that exact moment no error handler has been registered for the Promise.
For the cases where you want a rejected Promise to hold onto its rejected state for an indefinite amount of time before observing, you could call `defer()`, which suppresses automatic error reporting on that Promise.
If a Promise is rejected, it defaults to noisily reporting that fact to the developer console (instead of defaulting to silence). You can opt out of that reporting either implicitly (by registering an error handler before rejection), or explicitly (with `defer()`). In either case, you control the false positives.

Consider:

```javascript
var p = Promise.reject( "Oops" ).defer();

// `foo(..)` is Promise-aware
foo( 42 )
.then(
  function fulfilled(){
    return p;
  },
  function rejected(err){
    // handle `foo(..)` error
  }
);
```

When we create p, we know we're going to wait a while to use/observe its rejection, so we call `defer()` -- thus no global reporting. `defer()` simply returns the same promise, for chaining purposes.

The promise returned from `foo(..)` gets an error handler attached right away, so it's implicitly opted out and no global reporting for it occurs either.

But the promise returned from the `then(..)` call has no `defer()` or error handler attached, so if it rejects (from inside either resolution handler), then it will be reported to the developer console as an uncaught error.

This design is a pit of success. By default, all errors are either handled or reported -- what almost all developers in almost all cases would expect. You either have to register a handler or you have to intentionally opt out, and indicate you intend to defer error handling until later; you're opting for the extra responsibility in just that specific case.

The only real danger in this approach is if you `defer()` a Promise but then fail to actually ever observe/handle its rejection.

But you had to intentionally call `defer()` to opt into that pit of despair -- the default was the pit of success -- so there's not much else we could do to save you from your own mistakes.

I think there's still hope for Promise error handling (post-ES6). I hope the powers that be will rethink the situation and consider this alternative. In the meantime, you can implement this yourself (a challenging exercise for the reader!), or use a smarter Promise library that does so for you!

Note: This exact model for error handling/reporting is implemented in my asynquence Promise abstraction library, which will be discussed in Appendix A of this book.

### Promise Patterns

We've already implicitly seen the sequence pattern with Promise chains (this-then-this-then-that flow control) but there are lots of variations on asynchronous patterns that we can build as abstractions on top of Promises. These patterns serve to simplify the expression of async flow control -- which helps make our code more reason-able and more maintainable -- even in the most complex parts of our programs.

Two such patterns are codified directly into the native ES6 Promise implementation, so we get them for free, to use as building blocks for other patterns.

#### Promise.all([ .. ])

In an async sequence (Promise chain), only one async task is being coordinated at any given moment -- step 2 strictly follows step 1, and step 3 strictly follows step 2. But what about doing two or more steps concurrently (aka "in parallel")?

In classic programming terminology, a "gate" is a mechanism that waits on two or more parallel/concurrent tasks to complete before continuing. It doesn't matter what order they finish in, just that all of them have to complete for the gate to open and let the flow control through.

In the Promise API, we call this pattern all([ .. ]).

Say you wanted to make two Ajax requests at the same time, and wait for both to finish, regardless of their order, before making a third Ajax request. Consider:

```javascript
// `request(..)` is a Promise-aware Ajax utility,
// like we defined earlier in the chapter

var p1 = request( "http://some.url.1/" );
var p2 = request( "http://some.url.2/" );

Promise.all( [p1,p2] )
.then( function(msgs){
  // both `p1` and `p2` fulfill and pass in
  // their messages here
  return request(
    "http://some.url.3/?v=" + msgs.join(",")
  );
} )
.then( function(msg){
  console.log( msg );
} );
```

`Promise.all([ .. ])` expects a single argument, an array, consisting generally of Promise instances. The promise returned from the `Promise.all([ .. ])` call will receive a fulfillment message (msgs in this snippet) that is an array of all the fulfillment messages from the passed in promises, in the same order as specified (regardless of fulfillment order).

Note: Technically, the array of values passed into `Promise.all([ .. ])` can include Promises, thenables, or even immediate values. Each value in the list is essentially passed through `Promise.resolve(..)` to make sure it's a genuine Promise to be waited on, so an immediate value will just be normalized into a Promise for that value. If the array is empty, the main Promise is immediately fulfilled.

The main promise returned from `Promise.all([ .. ])` will only be fulfilled if and when all its constituent promises are fulfilled. If any one of those promises instead is rejected, the main `Promise.all([ .. ])` promise is immediately rejected, discarding all results from any other promises.

Remember to always attach a rejection/error handler to every promise, even and especially the one that comes back from `Promise.all([ .. ])`.

#### Promise.race([ .. ])

While `Promise.all([ .. ])` coordinates multiple Promises concurrently and assumes all are needed for fulfillment, sometimes you only want to respond to the "first Promise to cross the finish line," letting the other Promises fall away.

This pattern is classically called a "latch," but in Promises it's called a "race."

Warning: While the metaphor of "only the first across the finish line wins" fits the behavior well, unfortunately "race" is kind of a loaded term, because "race conditions" are generally taken as bugs in programs (see Chapter 1). Don't confuse `Promise.race([ .. ])` with "race condition".

`Promise.race([ .. ])` also expects a single array argument, containing one or more Promises, thenables, or immediate values. It doesn't make much practical sense to have a race with immediate values, because the first one listed will obviously win -- like a foot race where one runner starts at the finish line!

Similar to `Promise.all([ .. ])`, `Promise.race([ .. ])` will fulfill if and when any Promise resolution is a fulfillment, and it will reject if and when any Promise resolution is a rejection.

Warning: A "race" requires at least one "runner," so if you pass an empty array, instead of immediately resolving, the main race([..]) Promise will never resolve. This is a footgun! ES6 should have specified that it either fulfills, rejects, or just throws some sort of synchronous error. Unfortunately, because of precedence in Promise libraries predating ES6 Promise, they had to leave this gotcha in there, so be careful never to send in an empty array.

Let's revisit our previous concurrent Ajax example, but in the context of a race between p1 and p2:

```javascript
// `request(..)` is a Promise-aware Ajax utility,
// like we defined earlier in the chapter

var p1 = request( "http://some.url.1/" );
var p2 = request( "http://some.url.2/" );

Promise.race( [p1,p2] )
.then( function(msg){
  // either `p1` or `p2` will win the race
  return request(
    "http://some.url.3/?v=" + msg
  );
} )
.then( function(msg){
  console.log( msg );
} );
```

Because only one promise wins, the fulfillment value is a single message, not an array as it was for `Promise.all([ .. ])`.

##### Timeout Race

We saw this example earlier, illustrating how `Promise.race([ .. ])` can be used to express the "promise timeout" pattern:

```javascript
// `foo()` is a Promise-aware function

// `timeoutPromise(..)`, defined ealier, returns
// a Promise that rejects after a specified delay

// setup a timeout for `foo()`
Promise.race( [
  foo(),      // attempt `foo()`
  timeoutPromise( 3000 )  // give it 3 seconds
] )
.then(
  function(){
    // `foo(..)` fulfilled in time!
  },
  function(err){
    // either `foo()` rejected, or it just
    // didn't finish in time, so inspect
    // `err` to know which
  }
);
```

This timeout pattern works well in most cases. But there are some nuances to consider, and frankly they apply to both `Promise.race([ .. ])` and `Promise.all([ .. ])` equally.

##### "Finally"

The key question to ask is, "What happens to the promises that get discarded/ignored?" We're not asking that question from the performance perspective -- they would typically end up garbage collection eligible -- but from the behavioral perspective (side effects, etc.). Promises cannot be canceled -- and shouldn't be as that would destroy the external immutability trust discussed in the "Promise Uncancelable" section later in this chapter -- so they can only be silently ignored.

But what if `foo()` in the previous example is reserving some sort of resource for usage, but the timeout fires first and causes that promise to be ignored? Is there anything in this pattern that proactively frees the reserved resource after the timeout, or otherwise cancels any side effects it may have had? What if all you wanted was to log the fact that foo() timed out?

Some developers have proposed that Promises need a `finally(..)` callback registration, which is always called when a Promise resolves, and allows you to specify any cleanup that may be necessary. This doesn't exist in the specification at the moment, but it may come in ES7+. We'll have to wait and see.

It might look like:

```javascript
var p = Promise.resolve( 42 );

p.then( something )
.finally( cleanup )
.then( another )
.finally( cleanup );
```

Note: In various Promise libraries, `finally(..)` still creates and returns a new Promise (to keep the chain going). If the `cleanup(..)` function were to return a Promise, it would be linked into the chain, which means you could still have the unhandled rejection issues we discussed earlier.

In the meantime, we could make a static helper utility that lets us observe (without interfering) the resolution of a Promise:

```javascript
// polyfill-safe guard check
if (!Promise.observe) {
  Promise.observe = function(pr,cb) {
    // side-observe `pr`'s resolution
    pr.then(
      function fulfilled(msg){
        // schedule callback async (as Job)
        Promise.resolve( msg ).then( cb );
      },
      function rejected(err){
        // schedule callback async (as Job)
        Promise.resolve( err ).then( cb );
      }
    );

    // return original promise
    return pr;
  };
}
```

Here's how we'd use it in the timeout example from before:

```javascript
Promise.race( [
  Promise.observe(
    foo(),        // attempt `foo()`
    function cleanup(msg){
      // clean up after `foo()`, even if it
      // didn't finish before the timeout
    }
  ),
  timeoutPromise( 3000 )  // give it 3 seconds
] )
```

This `Promise.observe(..)` helper is just an illustration of how you could observe the completions of Promises without interfering with them. Other Promise libraries have their own solutions. Regardless of how you do it, you'll likely have places where you want to make sure your Promises aren't just silently ignored by accident.

#### Variations on all([ .. ]) and race([ .. ])

While native ES6 Promises come with built-in `Promise.all([ .. ])` and `Promise.race([ .. ])`, there are several other commonly used patterns with variations on those semantics:

- `none([ .. ])` is like `all([ .. ])`, but fulfillments and rejections are transposed. All Promises need to be rejected -- rejections become the fulfillment values and vice versa.
- `any([ .. ])` is like `all([ .. ])`, but it ignores any rejections, so only one needs to fulfill instead of all of them.
- `first([ .. ])` is like a race with `any([ .. ])`, which is that it ignores any rejections and fulfills as soon as the first Promise fulfills.
- `last([ .. ])` is like `first([ .. ])`, but only the latest fulfillment wins.

Some Promise abstraction libraries provide these, but you could also define them yourself using the mechanics of Promises, `race([ .. ])` and `all([ .. ])`.

For example, here's how we could define `first([ .. ])`:

```javascript
// polyfill-safe guard check
if (!Promise.first) {
  Promise.first = function(prs) {
    return new Promise( function(resolve,reject){
      // loop through all promises
      prs.forEach( function(pr){
        // normalize the value
        Promise.resolve( pr )
        // whichever one fulfills first wins, and
        // gets to resolve the main promise
        .then( resolve );
      } );
    } );
  };
}
```

Note: This implementation of `first(..)` does not reject if all its promises reject; it simply hangs, much like a `Promise.race([])` does. If desired, you could add additional logic to track each promise rejection and if all reject, call `reject()` on the main promise. We'll leave that as an exercise for the reader.

#### Concurrent Iterations

Sometimes you want to iterate over a list of Promises and perform some task against all of them, much like you can do with synchronous arrays (e.g., `forEach(..)`, `map(..)`, `some(..)`, and `every(..)`). If the task to perform against each Promise is fundamentally synchronous, these work fine, just as we used `forEach(..)` in the previous snippet.

But if the tasks are fundamentally asynchronous, or can/should otherwise be performed concurrently, you can use async versions of these utilities as provided by many libraries.

For example, let's consider an asynchronous `map(..)` utility that takes an array of values (could be Promises or anything else), plus a function (task) to perform against each. `map(..)` itself returns a promise whose fulfillment value is an array that holds (in the same mapping order) the async fulfillment value from each task:

```javascript
if (!Promise.map) {
  Promise.map = function(vals,cb) {
    // new promise that waits for all mapped promises
    return Promise.all(
      // note: regular array `map(..)`, turns
      // the array of values into an array of
      // promises
      vals.map( function(val){
        // replace `val` with a new promise that
        // resolves after `val` is async mapped
        return new Promise( function(resolve){
          cb( val, resolve );
        } );
      } )
    );
  };
}
```

Note: In this implementation of `map(..)`, you can't signal async rejection, but if a synchronous exception/error occurs inside of the mapping callback (cb(..)), the main `Promise.map(..)` returned promise would reject.

Let's illustrate using `map(..)` with a list of Promises (instead of simple values):

```javascript
var p1 = Promise.resolve( 21 );
var p2 = Promise.resolve( 42 );
var p3 = Promise.reject( "Oops" );

// double values in list even if they're in
// Promises
Promise.map( [p1,p2,p3], function(pr,done){
  // make sure the item itself is a Promise
  Promise.resolve( pr )
  .then(
    // extract value as `v`
    function(v){
      // map fulfillment `v` to new value
      done( v * 2 );
    },
    // or, map to promise rejection message
    done
  );
} )
.then( function(vals){
  console.log( vals );  // [42,84,"Oops"]
} );
```

### Promise Limitations

Many of the details we'll discuss in this section have already been alluded to in this chapter, but we'll just make sure to review these limitations specifically.

#### Sequence Error Handling

We covered Promise-flavored error handling in detail earlier in this chapter. The limitations of how Promises are designed -- how they chain, specifically -- creates a very easy pitfall where an error in a Promise chain can be silently ignored accidentally.

But there's something else to consider with Promise errors. Because a Promise chain is nothing more than its constituent Promises wired together, there's no entity to refer to the entire chain as a single thing, which means there's no external way to observe any errors that may occur.

If you construct a Promise chain that has no error handling in it, any error anywhere in the chain will propagate indefinitely down the chain, until observed (by registering a rejection handler at some step). So, in that specific case, having a reference to the last promise in the chain is enough (p in the following snippet), because you can register a rejection handler there, and it will be notified of any propagated errors:

```javascript
// `foo(..)`, `STEP2(..)` and `STEP3(..)` are
// all promise-aware utilities

var p = foo( 42 )
.then( STEP2 )
.then( STEP3 );
```

Although it may seem sneakily confusing, p here doesn't point to the first promise in the chain (the one from the foo(42) call), but instead from the last promise, the one that comes from the then(STEP3) call.

Also, no step in the promise chain is observably doing its own error handling. That means that you could then register a rejection error handler on p, and it would be notified if any errors occur anywhere in the chain:

```javascript
p.catch( handleErrors );
```

But if any step of the chain in fact does its own error handling (perhaps hidden/abstracted away from what you can see), your `handleErrors(..)` won't be notified. This may be what you want -- it was, after all, a "handled rejection" -- but it also may not be what you want. The complete lack of ability to be notified (of "already handled" rejection errors) is a limitation that restricts capabilities in some use cases.

It's basically the same limitation that exists with a `try..catch` that can catch an exception and simply swallow it. So this isn't a limitation unique to Promises, but it is something we might wish to have a workaround for.

Unfortunately, many times there is no reference kept for the intermediate steps in a Promise-chain sequence, so without such references, you cannot attach error handlers to reliably observe the errors.

#### Single Value

Promises by definition only have a single fulfillment value or a single rejection reason. In simple examples, this isn't that big of a deal, but in more sophisticated scenarios, you may find this limiting.

The typical advice is to construct a values wrapper (such as an object or array) to contain these multiple messages. This solution works, but it can be quite awkward and tedious to wrap and unwrap your messages with every single step of your Promise chain.

##### Splitting Values

Sometimes you can take this as a signal that you could/should decompose the problem into two or more Promises.

Imagine you have a utility foo(..) that produces two values (x and y) asynchronously:

function getY(x) {
	return new Promise( function(resolve,reject){
		setTimeout( function(){
			resolve( (3 * x) - 1 );
		}, 100 );
	} );
}

function foo(bar,baz) {
	var x = bar * baz;

	return getY( x )
	.then( function(y){
		// wrap both values into container
		return [x,y];
	} );
}

foo( 10, 20 )
.then( function(msgs){
	var x = msgs[0];
	var y = msgs[1];

	console.log( x, y );	// 200 599
} );
First, let's rearrange what foo(..) returns so that we don't have to wrap x and y into a single array value to transport through one Promise. Instead, we can wrap each value into its own promise:

function foo(bar,baz) {
	var x = bar * baz;

	// return both promises
	return [
		Promise.resolve( x ),
		getY( x )
	];
}

Promise.all(
	foo( 10, 20 )
)
.then( function(msgs){
	var x = msgs[0];
	var y = msgs[1];

	console.log( x, y );
} );
Is an array of promises really better than an array of values passed through a single promise? Syntactically, it's not much of an improvement.

But this approach more closely embraces the Promise design theory. It's now easier in the future to refactor to split the calculation of x and y into separate functions. It's cleaner and more flexible to let the calling code decide how to orchestrate the two promises -- using Promise.all([ .. ]) here, but certainly not the only option -- rather than to abstract such details away inside of foo(..).

## Source

Most of this was copied with minor edits from "You dont know JS" by Kyle Simpson
