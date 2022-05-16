---
id: xvbbugpzluf1p5xzpqax7fn
title: Responsive Image
desc: 'Notes on CSS Responsive Images'
updated: 1652683954779
created: 1652678718553
---
## Basic Responsiveness

- Do not set width
- Set height to auto

## Background Image

```css
background-position: center;
background-size: cover
```

## Object Fit Property

Works on `<img>` tags

```css
object-fit: cover;
```

or

```css
object-fit: contain;
```

## SRCSETs

The srcset and sizes attributes look complicated, but they're not too hard to understand if you format them as shown below, with a different part of the attribute value on each line. Each value contains a comma-separated list, and each part of those lists is made up of three sub-parts.

```html
<img srcset="elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 600px) 480px,
            800px"
     src="elva-fairy-800w.jpg"
     alt="Elva dressed as a fairy">
```

`srcset` defines the set of images we will allow the browser to choose between, and what size each image is. Each set of image information is separated from the previous one by a comma. For each one, we write:

1. An image filename (elva-fairy-480w.jpg)
2. A space
3. The image's intrinsic width in pixels (480w) — note that this uses the w unit, not px as you might expect. An image's intrinsic size is its real size, which can be found by inspecting the image file on your computer (for example, on a Mac you can select the image in Finder and press Cmd + I to bring up the info screen).

`sizes` defines a set of media conditions (e.g. screen widths) and indicates what image size would be best to choose, when certain media conditions are true — these are the hints we talked about earlier. In this case, before each comma we write:

1. A media condition ((max-width:600px)) — you'll learn more about these in the CSS topic, but for now let's just say that a media condition describes a possible state that the screen can be in. In this case, we are saying "when the viewport width is 600 pixels or less".
2. A space
3. The width of the slot the image will fill when the media condition is true (480px)

### SRCSET Resolution Switching: Same size, different resolutions

If you're supporting multiple display resolutions, but everyone sees your image at the same real-world size on the screen, you can allow the browser to choose an appropriate resolution image by using srcset with x-descriptors and without sizes — a somewhat easier syntax!

```html
<img srcset="elva-fairy-320w.jpg,
             elva-fairy-480w.jpg 1.5x,
             elva-fairy-640w.jpg 2x"
     src="elva-fairy-640w.jpg"
     alt="Elva dressed as a fairy">
```

In this example, the following CSS is applied to the image so that it will have a width of 320 pixels on the screen (also called CSS pixels):

```css
img {
    width: 320px;
}
```

In this case, sizes is not needed — the browser works out what resolution the display is that it is being shown on, and serves the most appropriate image referenced in the srcset. So if the device accessing the page has a standard/low resolution display, with one device pixel representing each CSS pixel, the `elva-fairy-320w.jpg` image will be loaded (the 1x is implied, so you don't need to include it.) If the device has a high resolution of two device pixels per CSS pixel or more, the `elva-fairy-640w.jpg` image will be loaded. The 640px image is 93KB, whereas the 320px image is only 39KB.

## `<Picture>` Element

The `<picture>` element is a wrapper containing several `<source>` elements that provide different sources for the browser to choose from, followed by the all-important `<img>` element.

```html
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```

- The `<source>` elements include a media attribute that contains a media condition — as with the first srcset example, these conditions are tests that decide which image is shown — the first one that returns true will be displayed. In this case, if the viewport width is 799px wide or less, the first `<source>` element's image will be displayed. If the viewport width is 800px or more, it'll be the second one.
- The srcset attributes contain the path to the image to display. Just as we saw with `<img>` above, `<source>` can take a srcset attribute with multiple images referenced, as well as a sizes attribute. So, you could offer multiple images via a `<picture>` element, but then also offer multiple resolutions of each one. Realistically, you probably won't want to do this kind of thing very often.
- In all cases, you must provide an `<img>` element, with src and alt, right before `</picture>`, otherwise no images will appear. This provides a default case that will apply when none of the media conditions return true (you could actually remove the second `<source>` element in this example), and a fallback for browsers that don't support the `<picture>` element.

## Reference Links

[CSS Tricks Article](https://css-tricks.com/a-guide-to-the-responsive-images-syntax-in-html/)

[MDN Page](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)