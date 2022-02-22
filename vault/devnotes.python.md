---
id: THqFYHlDTguT4tBejc3TH
title: Python
desc: 'Python Notes'
updated: 1645477664350
created: 1644000888615
---
Documentation Site for Python

Numpy, scipy, sympy PyYAML Pandas jmespath python-dateutil pytest

underscore _ gets you the previous result

formatted string literals - f-strings

print() has some unique arguments to change its default behavior: ```sep``` and ```end```

```Python
print("Hello")
print("World")
```

Will append a ```/n``` newline at the end resulting in:

> Hello
>
> World

you can change this to on line by:

```Python
print("Hello", end="")
print("World")
```

> HelloWorld

for an example of `sep`:

```python
print("cat", "dog", "mouse")
```

standard behavior is to add a space as a separator between array items:

> cat dog mouse

you can use `sep` to change this behavior

```python
print("cat", "dog", "mouse", sep="ABC")
```

> catABCdogABCmouse

Mutable values are not stored in the variable just a **reference** to them which means that they can be cross modified ie:

```python
>>> spam = [1, 2, 3, 4]
>>> cheese = spam
>>> cheese[1] = "Hello"
>>> cheese 
[1, "Hello", 2, 3, 4]
>>> spam 
[1, "Hello", 2, 3, 4]
```

Immutable values such as strings or tuples cannot be modified unless they are replaced.

You can also use `copy.deepcoopy(spam)` to create a new list with a new reference.
