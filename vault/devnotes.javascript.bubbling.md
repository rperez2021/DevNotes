---
id: 1nwnk5e8e9yluffevhwlajo
title: Bubbling
desc: 'Understanding Bubbling'
updated: 1646366413933
created: 1646365815256
---
## General Info

Event listeners will bubble up if they are listening to multiple levels of the DOM when you click on a nested element and trigger any other event listeners on parent items.

## Quick Links

[Wes Bos Video](https://www.youtube.com/watch?v=F1anRyL37lE)

## Sample Code

HTML

```html 
  <div class="one">
    <div class="two">
      <div class="three">
      </div>
    </div>
  </div>
```

JS

```Javascript
const divs = document.querySelectorAll('div');
const button = document.querySelector('button');

  function logText(e) {
    console.log(this.classList.value);
    e.stopPropagation(); // stops bubbling!
    console.log(this);
  }
```
