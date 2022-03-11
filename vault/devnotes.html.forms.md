---
id: smi7awfud2kinnlso6h5od4
title: Forms
desc: 'Notes on Forms'
updated: 1646936922418
created: 1646860291008
---
## General Info

## Tips

Note: You can also use the `<input>` element with the corresponding type to produce a button, for example `<input type="submit">`. The main advantage of the `<button>` element is that the `<input>` element only allows plain text in its label whereas the `<button>` element allows full HTML content, allowing more complex, creative button content.

Many assistive technologies will use the `<legend>` element as if it is a part of the label of each control inside the corresponding `<fieldset>` element. For example, some screen readers such as Jaws and NVDA will speak the legend's content before speaking the label of each control.

Each time you have a set of radio buttons, you should nest them inside a `<fieldset>` element. There are other use cases, and in general the `<fieldset>` element can also be used to section a form.

Test forms you create on screen readers!

## Best Practices

[Best Practices from Smashing Magazine](https://www.smashingmagazine.com/2009/07/web-form-validation-best-practices-and-tutorials/)

Most field types are obvious, but there are exceptions. For example, credit cards are numeric, but the increment/decrement spinner is useless and it’s too easy to press up or down when entering a 16-digit number. It’s better to use a standard `text` type, but set the `inputmode` attribute to `numeric`, which shows an appropriate keyboard. Setting `autocomplete="cc-number"` also suggests any pre-configured or previously entered card numbers.

## Constraint Validation API

Extends the standard HTML form validation to other elements and provides JS support for different functions.

`<form novalidate>` will disable browser automatic validation and will allow validation scripts to take over.

Example Usage:

```html
<form>
  <label for="name">Enter username (upper and lowercase letters): </label>
  <input type="text" name="name" id="name" required pattern="[A-Za-z]+">
  <button>Submit</button>
</form>
```

The basic HTML form validation features will cause this to produce a default error message if you try to submit the form with either no value filled in, or a value that does not match the pattern.

If you wanted to instead display custom error messages, you could use JavaScript like the following:

```javascript
const nameInput = document.querySelector('input');

nameInput.addEventListener('input', () => {
  nameInput.setCustomValidity('');
  nameInput.checkValidity();
});

nameInput.addEventListener('invalid', () => {
  if(nameInput.value === '') {
    nameInput.setCustomValidity('Enter your username!');
  } else {
    nameInput.setCustomValidity('Usernames can only contain upper and lowercase letters. Try again!');
  }
});
```
