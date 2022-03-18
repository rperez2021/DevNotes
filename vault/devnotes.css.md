---
id: B07UdMhx2vwSI07fs2mpe
title: CSS
desc: ''
updated: 1647574393927
created: 1643994767068
---
## Cool Tools

[Browser Default Styles](https://browserdefaultstyles.com/)

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

![Alternate Box Model](/assets/images/alternate-box-model.png)

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

### Lists

```css
ul {
  /* To replace list marker with image */
  list-style-image: url('sqpurple.gif');
  /* To place list marker outside the list item, outside is default */
  list-style-position: inside;
  
}
```

### Tables

Removing double borders on tables:

```css
table {
  border-collapse: collapse;
}
```

Responsive Table: place the table in an element with `overflow-x: auto`

```css
<div style="overflow-x:auto;">

<table>
... table content ...
</table>

</div>
```

### Z-Index

z-index only works on positioned elements (position: absolute, position: relative, position: fixed, or position: sticky) and flex items (elements that are direct children of display: flex elements).

If two positioned elements overlap each other without a z-index specified, the element defined last in the HTML code will be shown on top.

### Clear-Fix Hack

If a floated element is taller than the containing element, it will "overflow" outside of its container.

```css
.clearfix::after {
  content: "";
  clear: both;
  display: table;
}
```

![Clearfix Problem](/assets/images/clearfix_prob.jpg)

![Clearfix Solution](/assets/images/clearfix_solution.jpg)

### Inline-Block

- Compared to `display: inline`, the major difference is that `display: inline-block` allows to set a width and height on the element.

- Also, with `display: inline-block`, the top and bottom margins/paddings are respected, but with `display: inline` they are not.

- Compared to `display: block`, the major difference is that `display: inline-block` does not add a line-break after the element, so the element can sit next to other elements.

<style>
span.a {
  display: inline; /*the default for span*/
  width: 100px;
  height: 100px;
  padding: 5px;
  border: 1px solid blue;  
  background-color: yellow;
  color: black;
}

span.b {
  display: inline-block;
  width: 100px;
  height: 100px;
  padding: 5px;
  border: 1px solid blue;
  background-color: yellow;
  color: black;
}

span.c {
  display: block;
  width: 100px;
  height: 100px;
  padding: 5px;
  border: 1px solid blue;
  background-color: yellow;
  color: black;
}
</style>
</head>
<body>

<h3>display: inline</h3>
<div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum consequat scelerisque elit sit amet consequat. Aliquam erat volutpat. <span class="a">Aliquam</span> <span class="a">venenatis</span> gravida nisl sit amet facilisis. Nullam cursus fermentum velit sed laoreet. </div>

<h3>display: inline-block</h3>
<div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum consequat scelerisque elit sit amet consequat. Aliquam erat volutpat. <span class="b">Aliquam</span> <span class="b">venenatis</span> gravida nisl sit amet facilisis. Nullam cursus fermentum velit sed laoreet. </div>

<h3>display: block</h3>
<div>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum consequat scelerisque elit sit amet consequat. Aliquam erat volutpat. <span class="c">Aliquam</span> <span class="c">venenatis</span> gravida nisl sit amet facilisis. Nullam cursus fermentum velit sed laoreet. </div>

</body>
</html>

### Centering Elements

**Center Align Element:** To horizontally center a block element (like `<div>`), use `margin: auto;` **Note**: Center aligning has no effect if the width property is not set (or set to 100%).

**Center Align Text:** To just center the text inside an element, use text-align: center;

**Center An Image:** To center an image, set left and right margin to auto and make it into a block element:

**Center Vertically:**

- Use bottom and top padding.

-You can also use `line-height` with a value equal to the height property of the element.

- If padding and line-height are not options, another solution is to use positioning and the transform property: `transform: translate(-50%, -50%);`

- You can also use flexbox to center things. Just note that flexbox is not supported in IE10 and earlier versions:

```css
.center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
  border: 3px solid green;
}
```

### CSS Combinators

#### Descendant Selector

```css
div p {
  background-color: yellow;
}
```

Selects all P elements inside a div.

#### Child Selector (>)

```css
div > p {
  background-color: yellow;
}
```

Selects all direct child P elements inside a div.

#### Adjacent Sibling Selector (+)

The adjacent sibling selector is used to select an element that is directly after another specific element.

```css
div + p {
  background-color: yellow;
}
```

Selects the first `<p>` element that are placed immediately after `<div>` elements

#### General Sibling Selector

The general sibling selector selects all elements that are next siblings of a specified element.

```css
div ~ p {
  background-color: yellow;
}
```

Selects all `<p>` elements that are next siblings of `<div>` elements:

### Pseudo Classes

A pseudo-class is used to define a special state of an element.

**Note:** `a:hover` MUST come after `a:link` and `a:visited` in the CSS definition in order to be effective! `a:active` MUST come after `a:hover` in the CSS definition in order to be effective!

Pseudo-class names are not case-sensitive.

`:first-child`

`:lang(es)` usage `<q lang="es">`

<table class="ws-table-all notranslate">
  <tbody><tr>
    <th style="width:20%">Selector</th>
    <th style="width:20%">Example</th>
    <th>Example description</th>
  </tr>
  <tr>
    <td>:active</td>
    <td>a:active</td>
    <td>Selects the active link</td>
  </tr>
  <tr>
    <td>:checked</td>
    <td>input:checked</td>
    <td>Selects every checked &lt;input&gt; element</td>
  </tr>
  <tr>
    <td>:disabled</td>
    <td>input:disabled</td>
    <td>Selects every disabled &lt;input&gt; element</td>
  </tr>
  <tr>
    <td>:empty</td>
    <td>p:empty</td>
    <td>Selects every &lt;p&gt; element that has no children</td>
  </tr>
  <tr>
    <td>:enabled</td>
    <td>input:enabled</td>
    <td>Selects every enabled &lt;input&gt; element</td>
  </tr>
  <tr>
    <td>:first-child</td>
    <td>p:first-child</td>
    <td>Selects every &lt;p&gt; elements that is the first child of its parent</td>
  </tr>
  <tr>
    <td>:first-of-type</td>
    <td>p:first-of-type</td>
    <td>Selects every &lt;p&gt; element that is the first &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:focus</td>
    <td>input:focus</td>
    <td>Selects the &lt;input&gt; element that has focus</td>
  </tr>
  <tr>
    <td>:hover</td>
    <td>a:hover</td>
    <td>Selects links on mouse over</td>
  </tr>
  <tr>
    <td>:in-range</td>
    <td>input:in-range</td>
    <td>Selects &lt;input&gt; elements with a value within a specified range</td>
  </tr>
  <tr>
    <td>:invalid</td>
    <td>input:invalid</td>
    <td>Selects all &lt;input&gt; elements with an invalid value</td>
  </tr>
  <tr>
    <td>:lang(<i>language</i>)</td>
    <td>p:lang(it)</td>
    <td>Selects every &lt;p&gt; element with a lang attribute value starting with "it"</td>
  </tr>
  <tr>
    <td>:last-child</td>
    <td>p:last-child</td>
    <td>Selects every &lt;p&gt; elements that is the last child of its parent</td>
  </tr>
  <tr>
    <td>:last-of-type</td>
    <td>p:last-of-type</td>
    <td>Selects every &lt;p&gt; element that is the last &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:link</td>
    <td>a:link</td>
    <td>Selects all unvisited links</td>
  </tr>
  <tr>
    <td>:not(selector)</td>
    <td>:not(p)</td>
    <td>Selects every element that is not a &lt;p&gt; element</td>
  </tr>
  <tr>
    <td>:nth-child(n)</td>
    <td>p:nth-child(2)</td>
    <td>Selects every &lt;p&gt; element that is the second child of its parent</td>
  </tr>
  <tr>
    <td>:nth-last-child(n)</td>
    <td>p:nth-last-child(2)</td>
    <td>Selects every &lt;p&gt; element that is the second child of its parent, counting from the last child</td>
  </tr>
  <tr>
    <td>:nth-last-of-type(n)</td>
    <td>p:nth-last-of-type(2)</td>
    <td>Selects every &lt;p&gt; element that is the second &lt;p&gt; element of its parent, counting from the last child</td>
  </tr>
  <tr>
    <td>:nth-of-type(n)</td>
    <td>p:nth-of-type(2)</td>
    <td>Selects every &lt;p&gt; element that is the second &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:only-of-type</a></td>
    <td>p:only-of-type</td>
    <td>Selects every &lt;p&gt; element that is the only &lt;p&gt; element of its parent</td>
  </tr>
  <tr>
    <td>:only-child</a></td>
    <td>p:only-child</td>
    <td>Selects every &lt;p&gt; element that is the only child of its parent</td>
  </tr>
  <tr>
    <td>:optional</a></td>
    <td>input:optional</td>
    <td>Selects &lt;input&gt; elements with no "required" attribute</td>
  </tr>
  <tr>
    <td>:out-of-range</a></td>
    <td>input:out-of-range</td>
    <td>Selects &lt;input&gt; elements with a value outside a specified range</td>
  </tr>
  <tr>
    <td>:read-only</a></td>
    <td>input:read-only</td>
    <td>Selects &lt;input&gt; elements with a "readonly" attribute specified</td>
  </tr>
  <tr>
    <td>:read-write</a></td>
    <td>input:read-write</td>
    <td>Selects &lt;input&gt; elements with no "readonly" attribute</td>
  </tr>
  <tr>
    <td>:required</a></td>
    <td>input:required</td>
    <td>Selects &lt;input&gt; elements with a "required" attribute specified</td>
  </tr>
  <tr>
    <td>:root</a></td>
    <td>root</td>
    <td>Selects the document's root element</td>
  </tr>
  <tr>
    <td>:target</a></td>
    <td>#news:target</td>
    <td>Selects the current active #news element (clicked on a URL containing that anchor name)</td>
  </tr>
  <tr>
    <td>:valid</a></td>
    <td>input:valid</td>
    <td>Selects all &lt;input&gt; elements with a valid value</td>
  </tr>
  <tr>
    <td>:visited</a></td>
    <td>a:visited</td>
    <td>Selects all visited links</td>
  </tr>
</tbody></table>

## Resizing Text

You can use `calc()` to create a resizing rule that keeps a baseline size but allows you to enlarge as the viewport increases.

```css
body {
  // font grows 1px for every 100px of viewport width
  font-size: calc(16px + 1vw);
  // leading grows along with font,
  // with an additional 0.1em + 0.5px per 100px of the viewport
  line-height: calc(1.1em + 0.5vw);
}
```

## Fluid Aspect Ratios

```css
/* full-width * aspect-ratio */
.full-width {
  width: 100vw;
  height: calc(100vw * (9/16));
}
```

## CSS Truncate

Allows you to truncate a line of text. [CSS Tricks Page](https://css-tricks.com/snippets/css/truncate-string-with-ellipsis/)

```css
.truncate {
  width: 250px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

## Opacity

If you dont want to apply opacity to child elements you can use RGBA colors instead of the `opacity` css property.
