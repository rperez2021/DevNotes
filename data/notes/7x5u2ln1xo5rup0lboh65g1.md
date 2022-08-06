## General Info

A JSON string can be stored in its own file, which is basically just a text file with an extension of .json, and a [[MIME type]] of application/json.

## JSON.parse()

When receiving data from a web server, the data is always a string. Parse the data with JSON.parse(), and the data becomes a JavaScript object.

### Parsing Dates

The reviver parameter is a function that checks each property, before returning the value. It can be used to parse things like dates:

```javascript
const text = '{"name":"John", "birth":"1986-12-14", "city":"New York"}';
const obj = JSON.parse(text, function (key, value) {
  if (key == "birth") {
    return new Date(value);
  } else {
    return value;
  }
});
```

### Parsing Functions

Functions are not allowed in JSON. If you need to include a function, write it as a string. Then do something like this:

```javascript
const text = '{"name":"John", "age":"function () {return 30;}", "city":"New York"}';
const obj = JSON.parse(text);
obj.age = eval("(" + obj.age + ")");
```

## JSON.stringify()

Convert a JavaScript object into a string with JSON.stringify().

## Json Formatter Site

To check if JSON is improperly formatted [use this site](https://jsonformatter.curiousconcept.com/)
