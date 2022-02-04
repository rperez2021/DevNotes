---
id: MN1UL4sEQihMMFAAsS2Cc
title: HTML
desc: ''
updated: 1644000799916
created: 1644000457258
---
You can use a `start` attribute when using ordered (numbered) lists to start at a different interger. If you want to start your list at number 10 simply do `<ol start="10">`
Ex:

```HTML
<ol start="10">
<li>This should be 10
<li>This should be 11
<li>This should be 12
</ol>
```

Apparently this does not work on Dendron.

On the same note `reversed` attribute flips the number order.

Also `value` can change the value on an individual `<li>` and change the following list items.

[Shay Howe's Lists Tutorial](https://learn.shayhowe.com/html-css/creating-lists/) has a bunch of uncommon use cases.
