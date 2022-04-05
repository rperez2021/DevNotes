---
id: ovy80ftrjfart13d9j5gzhq
title: Fetch API
desc: 'Notes on the Fetch API'
updated: 1649009640933
created: 1649009640933
---
## General Info

- Similar to XHR but with promises instead of callbacks.

## Sample Usage

```javascript
// url (required), options (optional)
fetch('https://davidwalsh.name/some/url', {
    method: 'get'
}).then(function(response) {

}).catch(function(err) {
    // Error :(
});
```
