---
id: B07UdMhx2vwSI07fs2mpe
title: CSS
desc: ''
updated: 1646717671089
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

### CSS Colors

3 Digit Hex Code: The 3-digit hex code can only be used when both the values (RR, GG, and BB) are the same for each components. So, if we have #ff00cc, it can be written like this: #f0c.

## Margins

### Margin Auto

Margin `auto` will center an element in the middle of the page.

### Margin Collapse

Only happens in top or bottom margins, if two consecutive elements have top or bottom margins they are not additive but the greater of the two will be displayed.
