---
id: p6phdngl7y9b1gpl434v50n
title: Tree Shaking
desc: 'Notes on JS Tree Shaking'
updated: 1648695331870
created: 1648695331870
---
## General Info

Tree shaking is a term commonly used within a JavaScript context to describe the removal of dead code.

It relies on the import and export statements in ES2015 to detect if code modules are exported and imported for use between JavaScript files.

In modern JavaScript applications, we use module bundlers (e.g., webpack or Rollup) to automatically remove dead code when bundling multiple JavaScript files into single files. This is important for preparing code that is production ready, for example with clean structures and minimal file size.
