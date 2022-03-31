---
id: x93x4xyexybghiozz4co7yk
title: Export
desc: ''
updated: 1648695492969
created: 1648695492969
---
## General Info

The export statement is used when creating JavaScript modules to export live bindings to functions, objects, or primitive values from the module so they can be used by other programs with the `import` statement. The value of an imported binding is subject to change in the module that exports it. When a module updates the value of a binding that it exports, the update will be visible in its imported value.

Exported modules are in strict mode whether you declare them as such or not. The export statement cannot be used in embedded scripts.

### Syntax

There are two types of exports:

1. Named Exports (Zero or more exports per module)
2. Default Exports (One per module)

```javascript
// Exporting individual features
export let name1, name2, …, nameN; // also var, const
export let name1 = …, name2 = …, …, nameN; // also var, const
export function functionName(){...}
export class ClassName {...}

// Export list
export { name1, name2, …, nameN };

// Renaming exports
export { variable1 as name1, variable2 as name2, …, nameN };

// Exporting destructured assignments with renaming
export const { name1, name2: bar } = o;

// Default exports
export default expression;
export default function (…) { … } // also class, function*
export default function name1(…) { … } // also class, function*
export { name1 as default, … };

// Aggregating modules
export * from …; // does not set the default export
export * as name1 from …; // ECMAScript® 2O20
export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
export { default, … } from …;
```

**Note:** The following is syntactically invalid despite its import equivalent:

```javascript
import DefaultExport from 'bar.js'; // Valid
export DefaultExport from 'bar.js'; // Invalid
export { default as DefaultExport } from 'bar.js'; // Correct Export
```
