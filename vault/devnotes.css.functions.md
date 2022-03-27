---
id: 2ngvq02pnz8bswezw7lgjxc
title: Functions
desc: Notes on CSS Functions
updated: 1647559251870
created: 1647557312527
---
## Use Cases

- [Web.dev Examples for min(), max() and clamp()](https://web.dev/min-max-clamp/)
- [MDN List of all CSS Functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions)

### calc()

- Mixing Units, ex:

```css
:root {
    --header: 3rem;
    --footer: 40px;
    --main: calc(100vh - calc(var(--header) + var(--footer)));
}
```

### min() & max()

- Allows you to set different types of behaviors based on elements current size.

```css
#iconHolder {
  width: min(150px, 100%);
  height: min(150px, 100%);
  box-sizing: border-box;
  border: 6px solid blue;
}
```

### clamp()

- Great way to make elements fluid and responsive. clamp() takes 3 values:

    1. the smallest value (320px)
    2. the ideal value (80vw)
    3. the largest value (60rem)

### conic-gradient()

- Cool Stuff

```css
background: conic-gradient( 
    red 6deg, orange 6deg 18deg, yellow 18deg 45deg, 
    green 45deg 110deg, blue 110deg 200deg, purple 200deg);
```

<div style="background: conic-gradient(red 6deg, orange 6deg 18deg, yellow 18deg 45deg, green 45deg 110deg, blue 110deg 200deg, purple 200deg);width:200px;height:200px" ></div>

### cross-fade
