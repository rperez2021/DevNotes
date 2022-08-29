---
id: vyyr4anebo5q2wxrmty3uce
title: Structured Clone Algorithm
desc: ''
updated: 1659846368605
created: 1659846347834
---
## General Info

The structured clone algorithm copies complex JavaScript objects. It is used internally when invoking structuredClone(), to transfer data between Workers via postMessage(), storing objects with IndexedDB, or copying objects for other APIs.

It clones by recursing through the input object while maintaining a map of previously visited references, to avoid infinitely traversing cycles.
