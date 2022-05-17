---
id: ixjdv6uobiiporkdddwteyb
title: Media Queries
desc: 'Notes on Media Queries'
updated: 1652725276982
created: 1652721139619
---
## General Info

With media queries it is possible to completely restyle your web projects based on the size of a user’s screen.

## Syntax

```css
body {
  margin: 24px;
}

@media (max-width: 600px) {
  body {
    margin: 8px;
  }
}
```

In the above example, margin is changed based on screen size. Specifically, on all screens below or equal to 600px, the margin will be 8px, and on all screens above 600px, it will be 24px.

## Best Practices

1. Limit Media Queries: minimize your media-query usage and rely more on the natural flexibility of your layouts.
2. Common Breakpoints:
    - < 600px Mobile
    - 600px - 1200px Tablet
    - `>` 1200px Desktop
    - `>` 2000px Ultra Wide
3. Zooming: in most browsers, zooming in on a webpage will change the effective resolution of that page.
4. Other Queries: `min-width` (screens larger than a given value), `max-height` & `min-height`

## More Complex Queries

### Combining Multiple Types of Features

```css
@media (min-width: 30em) and (orientation: landscape) { ... }
@media screen and (min-width: 30em) and (orientation: landscape) { ... }
```

### Testing for Multiple Queries

You can use a comma-separated list to apply styles when the user's device matches any one of various media types, features, or states. For instance, the following rule will apply its styles if the user's device has either a minimum height of 680px or is a screen device in portrait mode:

```css
@media (min-height: 680px), screen and (orientation: portrait) { ... }
```

Taking the above example, if the user had a printer with a page height of 800px, the media statement would return true because the first query would apply. Likewise, if the user were on a smartphone in portrait mode with a viewport height of 480px, the second query would apply and the media statement would still return true.

### Inverting a Query's Meaning

The not keyword inverts the meaning of an entire media query. It will only negate the specific media query it is applied to. (Thus, it will not apply to every media query in a comma-separated list of media queries.) The not keyword can't be used to negate an individual feature query, only an entire media query. The not is evaluated last in the following query:

```css
@media not all and (monochrome) { ... }
```

... so that the above query is evaluated like this:

```css
@media not (all and (monochrome)) { ... }
```

### Improving compatibility with older browsers

The only keyword prevents older browsers that do not support media queries with media features from applying the given styles. It has no effect on modern browsers.

```css
@media only screen and (color) { ... }
```
