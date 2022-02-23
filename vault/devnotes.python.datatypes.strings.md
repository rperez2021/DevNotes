---
id: wGXbodJIgcEVOuiVmXxEB
title: Strings
desc: 'Notes on Python Strings'
updated: 1645640398112
created: 1645635471771
---
## General Notes

Triple quotes `'''` allow you to make multiline strings.

You can use [] to get a specific letter of a strings.

You can check for string partials with `in`

Strings are immutable so any changes with methods must be reassigned for example:

```python
>>> spam = "Hello World!"
>>> spam.upper()
"HELLO WORLD!"
>>> spam
"Hello World!" # see how the value never changed. 
>>> spam = spam.upper() # here we reassign the value
>>> spam
"HELLO WORLD!" # now it works
```

.isalpha()
.isdecimal() - true if it is a number
.isspace() - true if it contains spaces
.isalum() - true if is alpha numeric
.istitle() - true if all starting letters have an uppercase

.startswith(param)
.endswith(param)
.join() ex:

```python
>>>','.join(['cats', 'rats', 'bats'])
'cats,rats,bats'
```

.split() does the opposite splits a string into a list.

.rjust(total length of string) & .ljust(total length of string) & .center(total length of string)

.strip() - removes white space
.lstrip() - removes left white space
.rstrip() - removes right white space

%s - coversion specifier
