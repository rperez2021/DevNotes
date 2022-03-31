---
id: y53znpyve0v5l8xs4f0tpjm
title: Import Module
desc: 'Notes on JS Import Module'
updated: 1648694724451
created: 1648694724451
---
## General Info

The name parameter is the name of the "module object" which will be used as a kind of namespace to refer to the exports. The export parameters specify individual named exports, while the import * as name syntax imports all of them.

```javascript
import * as myModule from '/modules/my-module.js';

myModule.doAllTheAmazingThings();
```

### Import a single export from a module

```javascript
import {myExport} from '/modules/my-module.js';
```

### Import an export with a more convenient alias

```javascript
import {reallyReallyLongModuleExportName as shortName}
  from '/modules/my-module.js';
```

### Importing defaults

```javascript
import myDefault from '/modules/my-module.js';
```

It is also possible to use the default syntax with the ones seen above (namespace imports or named imports). In such cases, the default import will have to be declared first. For instance:

```javascript
import myDefault, * as myModule from '/modules/my-module.js';
// myModule used as a namespace
// OR:
import myDefault, {foo, bar} from '/modules/my-module.js';
// specific, named imports
```

## Dynamic Imports

The standard import syntax is static and will always result in all code in the imported module being evaluated at load time. In situations where you wish to load a module conditionally or on demand, you can use a dynamic import instead. The following are some reasons why you might need to use dynamic import:

- When importing statically significantly slows the loading of your code and there is a low likelihood that you will need the code you are importing, or you will not need it until a later time.
- When importing statically significantly increases your program's memory usage and there is a low likelihood that you will need the code you are importing.
- When the module you are importing does not exist at load time
- When the import specifier string needs to be constructed dynamically. (Static import only supports static specifiers.)
- When the module being imported has side effects, and you do not want those side effects unless some condition is true. (It is recommended not to have any side effects in a module, but you sometimes cannot control this in your module dependencies.)

Use dynamic import only when necessary. The static form is preferable for loading initial dependencies, and can benefit more readily from static analysis tools and tree shaking.

To dynamically import a module, the import keyword may be called as a function. When used this way, it returns a promise.

```javascript
import('/modules/my-module.js')
  .then((module) => {
    // Do something with the module.
  });
```

This form also supports the await keyword.

```javascript
let module = await import('/modules/my-module.js');
```

Dynamic Import Example:

```javascript
const main = document.querySelector("main");
for (const link of document.querySelectorAll("nav > a")) {
  link.addEventListener("click", e => {
    e.preventDefault();

    import('/modules/my-module.js')
      .then(module => {
        module.loadPageInto(main);
      })
      .catch(err => {
        main.textContent = err.message;
      });
  });
}
```
