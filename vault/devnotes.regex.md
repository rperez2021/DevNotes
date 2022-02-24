---
id: bym2AxoiHmKfMAdpOeBm9
title: Regex
desc: 'Regular Expressions Notes'
updated: 1645643611157
created: 1644602665546
---
## General Info

## Javascript Specific

```/g``` flag allows you to do a global search for example for ```text.replace(textToReplace/g, newText)``` without the ```/g``` it would return only the first match.

```/i``` flag will make you search match case insensitive

## Python Specific

import `re` module which is the regex library for python

```python
phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
mo = phoneNumRegex.search(string)
print(mo.group())
```
