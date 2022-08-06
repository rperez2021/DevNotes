## General Info

XML is case-sensitive (unlike HTML).

Attribute values in SVG must be placed inside quotes, even if they are numbers.

### Anatomy of an SVG

`xmlns` namespace attribute, tells browser what time of xml file this is

`viewbox` defines the bounds of the svg

## Inline vs Linked SVGs

Linking is generally cleaner and simpler but does not allow you to interact with the SVG through CSS or JavaScript.

Inlining SVGs allow you to unlock their full potential, but it also comes with some serious drawbacks: it makes your code harder to read, makes your page less cacheable, and if it’s a large SVG it might delay the rest of your HTML from loading.

## SVG Sites

[SVG Path Editor Tool](https://yqnn.github.io/svg-path-editor/)

### Icon Sites

[The Noun Project](https://thenounproject.com/)

[Feather Icons](https://feathericons.com/)

[Material Icons](https://fonts.google.com/icons)

## SVG Libraries

[SVGJS](https://svgjs.dev/docs/3.0/)

[SnapSVG](http://snapsvg.io/)
