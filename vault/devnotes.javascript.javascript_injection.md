---
id: ejsuf0yamyfbhaz9psry4if
title: Javascript_injection
desc: Notes on JS Injection
updated: 1646260845678
created: 1646260573772
---
## General Info

If `element.innerHTML` is being used you can inject javascript through an input field with a img tag like this:

`<img src onerror="alert('hacked')">`

If that input field manipulates a url you can do all sorts of bad stuff.

You can fix this by using innerText or TextContent
