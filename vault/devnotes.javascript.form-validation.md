---
id: ckrjovepsovc04yzrryo8w4
title: Form Validation
desc: 'Notes on JS Form Validation'
updated: 1648932014108
created: 1648932014108
---
## General Info

### novalidate

The `novalidate` attribute to turn off the browser's automatic validation; this lets our script take control over validation. However, this doesn't disable support for the constraint validation API nor the application of CSS pseudo-classes like `:valid`, etc. That means that even though the browser doesn't automatically check the validity of the form before sending its data, you can still do it yourself and style the form accordingly.

```html
<form novalidate>
</form>
```
