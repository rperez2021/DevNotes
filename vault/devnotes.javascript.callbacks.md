---
id: 88axwcjbb82fjakboxgydsg
title: Callback Functions
desc: 'Notes on Callback Functions'
updated: 1649272239514
created: 1648944376567
---
## General Info

A simple callback function in an event handler:

```javascript
myDiv.addEventListener("click", function(){
  // do something!
})
```

## Callback Hell

```javascript
fs.readdir(source, function (err, files) {
  if (err) {
    console.log('Error finding files: ' + err)
  } else {
    files.forEach(function (filename, fileIndex) {
      console.log(filename)
      gm(source + filename).size(function (err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err)
        } else {
          console.log(filename + ' : ' + values)
          aspect = (values.width / values.height)
          widths.forEach(function (width, widthIndex) {
            height = Math.round(width / aspect)
            console.log('resizing ' + filename + 'to ' + height + 'x' + height)
            this.resize(width, height).write(dest + 'w' + width + '_' + filename, function(err) {
              if (err) console.log('Error writing file: ' + err)
            })
          }.bind(this))
        }
      })
    })
  }
})
```

### Tips to Fix Callback Hell

1. Keep your code shallow

    Instead of this:

    ```javascript
    var form = document.querySelector('form')
    form.onsubmit = function (submitEvent) {
    var name = document.querySelector('input').value
    request({
        uri: "http://example.com/upload",
        body: name,
        method: "POST"
    }, function (err, response, body) {
        var statusMessage = document.querySelector('.status')
        if (err) return statusMessage.value = err
        statusMessage.value = body
    })
    }
    ```

    do this:

    ```javascript
    document.querySelector('form').onsubmit = formSubmit

    function formSubmit (submitEvent) {
    var name = document.querySelector('input').value
    request({
        uri: "http://example.com/upload",
        body: name,
        method: "POST"
    }, postResponse)
    }

    function postResponse (err, response, body) {
    var statusMessage = document.querySelector('.status')
    if (err) return statusMessage.value = err
    statusMessage.value = body
    }
    ```

2. Modularize

    Write small modules that each do one thing, and assemble them into other modules that do a bigger thing. You can't get into callback hell if you don't go there.

3. Handle Every Single Error

    There are different types of errors: syntax errors caused by the programmer (usually caught when you try to first run the program), runtime errors caused by the programmer (the code ran but had a bug that caused something to mess up), platform errors caused by things like invalid file permissions, hard drive failure, no network connection etc. This section is only meant to address this last class of errors.

    The first two rules are primarily about making your code readable, but this one is about making your code stable. When dealing with callbacks you are by definition dealing with tasks that get dispatched, go off and do something in the background, and then complete successfully or abort due to failure. Any experienced developer will tell you that you can never know when these errors happen, so you have to plan on them always happening.

    With callbacks the most popular way to handle errors is the Node.js style where the first argument to the callback is always reserved for an error.

    ```javascript
    var fs = require('fs')

    fs.readFile('/Does/not/exist', handleFile)

    function handleFile (error, file) {
    if (error) return console.error('Uhoh, there was an error', error)
    // otherwise, continue on and use `file` in your code
    }
    ```

### Example of NodeJS CallBack With FS

```javascript
var fs = require('fs')
var myNumber = undefined

function addOne(callback) {
  fs.readFile('number.txt', function doneReading(err, fileContents) {
    myNumber = parseInt(fileContents)
    myNumber++
    callback()
  })
}

function logMyNumber() {
  console.log(myNumber)
}

addOne(logMyNumber)
```

To break down this example even more, here is a timeline of events that happen when we run this program:

1. The code is parsed, which means if there are any syntax errors they would make the program break. During this initial phase, fs and myNumber are declared as variables while addOne and logMyNumber are declared as functions. Note that these are just declarations. Neither function has been called nor invoked yet.
2. When the last line of our program gets executed addOne is invoked with the logMyNumber function passed as its callback argument. Invoking addOne will first run the asynchronous fs.readFile function. This part of the program takes a while to finish.
3. With nothing to do, node idles for a bit as it waits for readFile to finish. If there was anything else to do during this time, node would be available for work.
4. As soon as readFile finishes it executes its callback, doneReading, which parses fileContents for an integer called myNumber, increments myNumber and then immediately invokes the function that addOne passed in (its callback), logMyNumber.

## Function Definition not Function Call

```javascript
function fullName(firstName, lastName, callback){
  console.log("My name is " + firstName + " " + lastName);
  callback(lastName);
}

// NOT
function fullName(firstName, lastName, callback()){
  console.log("My name is " + firstName + " " + lastName);
  callback(lastName);
}
```

We are passing the function definition, not the function call. This prevents the callback from being executed immediately, which is not the idea behind the callbacks.

The callback can be an existing function as shown in the preceding example, or it can be an anonymous function, which we create when we call the higher-order function, as shown in the following example:
