---
id: phnjc5yteyb5cb878n3eh10
title: Transform
desc: 'Notes on CSS Transform'
updated: 1651381986873
created: 1651255969294
---
## Chained Transforms

The transform functions are multiplied in order from left to right, meaning that composite transforms are e6ffectively applied in order from right to left.

### Chained Transform Example

```html
<div class="red-box"></div>
<div class="blue-box"></div>
```

```css
.red-box,
.blue-box {
  position: absolute;
  width: 100px;
  height: 100px;
}

.red-box {
  background: red;
  transform: rotate(45deg) translate(200%);
}

.blue-box {
  background: blue;
  transform: translate(200%) rotate(45deg);
}
```

Here is the result:

![Chain CSS Transform Result](/assets/css-chaining-transform.png)
