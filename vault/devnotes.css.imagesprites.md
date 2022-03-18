---
id: 64bcz5fld2n38w83wmee38x
title: Image Sprites
desc: 'Image Sprites Notes'
updated: 1647573716457
created: 1647572699543
---
## General Info

![Image Sprites](/assets/images/img_navsprites_hover.gif)

You can use an image sprite to reduce the number of requests done for images and then use css to select a part of the sprite for your image. Here is an example

```css
#home {
  width: 46px; /* Width of the Sprite You Want Selected */
  height: 44px; /* Height of the Sprite You Want Selected */
  background: url(img_navsprites.gif) 0 0; /* Image has to be pulled as a background for this to work, the numbers at the end indicate location of the sprite in x(left) and y(top) axis */
}


#next {
  width: 46px; 
  height: 44px; 
  background: url(img_navsprites.gif) 46 0; 
  }
```
