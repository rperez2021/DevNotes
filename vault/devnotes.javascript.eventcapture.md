---
id: l1lhl7tfi70qrdit0vtsfpo
title: Eventcapture
desc: Notes on Event Capture in JavaScript
updated: 1646366757523
created: 1646366005564
---
## General Info

Capture is a parameter that can be passed into an event listener. The parameter takes a boolean value indicating that events of this type will be dispatched to the registered listener before being dispatched to any EventTarget beneath it in the DOM tree. If not specified, defaults to false.

## Quick Links

[MDN for addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)

[Wes Bos 30 Days of JS Video](https://www.youtube.com/watch?v=F1anRyL37lE)

## Sample Code

```javascript
  divs.forEach(div => div.addEventListener('click', callback, {
    capture: false,
    once: true
  }));
```
