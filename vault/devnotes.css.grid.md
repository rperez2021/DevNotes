---
id: gwtxdrn8mqjq8p2u9c5s8ja
title: Grid
desc: Notes on CSS Grid
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

## Implicit Grid

If we add additional items from to those defined in the template they will be placed on the grid but they will not have explicit size values assigned to them unless you use `grid-auto-rows: 50px;` css property.

## Span

Grid defaults to spanning one track. You can use the span keyword when setting up grid columns or rows to extend the length based on the number of spans. For example:

```css
.box1 {
    grid-column: 1;
    grid-row: 1 / span 3;
}
```

## Grid Area Property

Shorthand for:

- grid-row-start
- grid-column-start
- grid-row-end
- grid-column-end

```css
.box1 {
   grid-area: 1 / 1 / 4 / 2;
}
```

## The Repeat CSS Function

```css
.grid-container {
  grid-template-rows: 150px 150px;
  grid-template-columns: 150px 150px 150px 150px 150px;
}
```

can be written as

```css
.grid-container {
  grid-template-rows: repeat(2, 150px);
  grid-template-columns: repeat(5, 150px);
}
```
