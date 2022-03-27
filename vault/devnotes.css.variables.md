---
id: 4k8jx70ww4gqow8k56wlevp
title: CSS Variables
desc: Notes on CSS Variables
updated: 1647829218145
created: 1647828444135
---
## CSS Variable Scope

Similar to Scope in JS, where the variable is decalred in the HTML tree defines where it can be used within that element or its children but does not work on its sibling or parent elements.

## Theme Example

```javascript
function setTheme() {
  const root = document.documentElement;
  const newTheme = root.className === 'dark' ? 'light' : 'dark';
  root.className = newTheme;
  
  document.querySelector('.theme-name').textContent = newTheme;
}

document.querySelector('.theme-toggle').addEventListener('click', setTheme)
```

```css
:root.dark{
  --border-btn: 1px solid rgb(220, 220, 220);
  --color-base-bg: rgb(18, 18, 18);
  --color-base-text: rgb(240, 240, 240);
  --color-btn-bg: rgb(36, 36, 36);
}

:root.light {
  --border-btn: 1px solid rgb(36, 36, 36);
  --color-base-bg: rgb(240, 240, 240);
  --color-base-text: rgb(18, 18, 18);
  --color-btn-bg: rgb(220, 220, 220);
}
```

## User Agent Theme with Media Query

```css
@media (prefers-color-scheme: dark) {
  :root {
    --border-btn: 1px solid rgb(220, 220, 220);
    --color-base-bg: rgb(18, 18, 18);
    --color-base-text: rgb(240, 240, 240);
    --color-btn-bg: rgb(36, 36, 36);
    --theme-name: "dark";
  }
}
```
