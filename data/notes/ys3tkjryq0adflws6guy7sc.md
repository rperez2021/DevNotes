
## Attribute Spaced Selector

At times attribute values may be spaced apart, in which only one of the words needs to be matched in order to make a selection. In this event using the tilde character, ~, within the square brackets of a selector between the attribute name and equals sign denotes an attribute value that should be whitespace-separated, with one word matching the exact stated value.

```css
a[rel~="tag"] {...}
```

```html
<a href="#" rel="tag nofollow">...</a>
```

## Attribute Hyphenated Selector

When an attribute value is hyphen-separated, rather than whitespace-separated, the vertical line character, |, may be used within the square brackets of a selector between the attribute name and equals sign. The vertical line denotes that the attribute value may be hyphen-separated however the hyphen-separated words must begin with the stated value.

```css
a[lang|="en"] {...}
```

```html
<a href="#" lang="en-US">...</a>
```

## Negative Pseudo-class Numbers & Expressions

To make things a bit more complicated negative numbers may also be used. For example, the li:nth-child(6n-4) selector will start counting every sixth list item starting at negative four, selecting the second, eighth, and fourteenth list items and so forth. The same selector, li:nth-child(6n-4), could also be written as li:nth-child(6n+2), without the use of a negative b variable.

A negative a variable, or a negative n argument, must be followed by a positive b variable. When preceded by a negative a variable or negative n argument the b variable identifies how high the counting will reach. For example, the li:nth-child(-3n+12) selector will select every third list item within the first twelve list items. The selector li:nth-child(-n+9) will select the first nine list items within a list, as the n argument, without any stated a variable, is defaulted to -1.

## Target Pseudo-class

The :target pseudo-class is used to style elements when an element’s ID attribute value matches that of the URI fragment identifier. The fragment identifier within a URI can be recognized by the hash character, #, and what directly follows it. The URL [http://example.com/index.html#hello](http://example.com/index.html#hello) includes the fragment identifier of hello. When this identifier matches the ID attribute value of an element on the page, `<section id="hello">` for example, that element may be identified and stylized using the `:target` pseudo-class. Fragment identifiers are most commonly seen when using on page links, or linking to another part of the same page.

## Textual Pseudo-elements

The first pseudo-elements ever released were the :first-letter and :first-line textual pseudo-elements. The :first-letter pseudo-element will identify the first letter of text within an element, while the :first-line pseudo-element will identify the first line of text within an element.
