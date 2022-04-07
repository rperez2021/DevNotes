---
id: ovy80ftrjfart13d9j5gzhq
title: Fetch API
desc: 'Notes on the Fetch API'
updated: 1649305388415
created: 1649009640933
---
## General Info

The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. It also provides a global fetch() method that provides an easy, logical way to fetch resources asynchronously across the network.

This kind of functionality was previously achieved using XMLHttpRequest. Fetch provides a better alternative that can be easily used by other technologies such as Service Workers. Fetch also provides a single logical place to define other HTTP-related concepts such as CORS and extensions to HTTP.

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
