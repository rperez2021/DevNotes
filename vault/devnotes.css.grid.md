---
id: gwtxdrn8mqjq8p2u9c5s8ja
title: Grid
desc: 'Notes on CSS Grid'
updated: 1647986737223
created: 1647986737223
---
## Grid Template Shorthand

```css
.container {
  display: grid;
  grid-template: 50px 50px / 50px 50px 50px;
}
```

is the same as:

```css
.container {
  display: grid;
  grid-template-columns: 50px 50px 50px;
  grid-template-rows: 50px 50px;
}
```
