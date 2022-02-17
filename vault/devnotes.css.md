---
id: B07UdMhx2vwSI07fs2mpe
title: CSS
desc: ''
updated: 1644002721465
created: 1643994767068
---
### Box Model

Margin collapses between elements.

### Standard Box Model

![Standard Box Model](/assets/images/2022-02-04-09-19-24.png)

Alternate Box Model

```CSS
html {
  box-sizing: border-box;
}
*, *::before, *::after {
  box-sizing: inherit;
}
```

![Alternate Box Model](/assets/images/2022-02-04-09-19-24.png)

**Note:** The margin is not counted towards the actual size of the box — sure, it affects the total space that the box will take up on the page, but only the space outside the box. The box's area stops at the border — it does not extend into the margin.

### Flex Box

Centered on X and Y axis `justify-content: center` is the X axis `align-items: center` is the Y axis if the `flex-direction` is default `flex-direction: row`

```CSS
.box {
  display: flex;
  align-items: center;
  justify-content: center;
}

.box div {
  width: 50px;
  height: 50px;
}
```

```HTML
<div class="box">
  <div></div>
</div>
```
