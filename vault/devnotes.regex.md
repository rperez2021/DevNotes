---
id: bym2AxoiHmKfMAdpOeBm9
title: Regex
desc: Regular Expressions Notes
updated: 1647456255440
created: 1644602665546
---
## General Info

[Regular Expression Multi Language Info Site](https://www.regular-expressions.info/)

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

`.group()` is a method to split a regex into smaller parts to filter for.

Groups are created in regex strings with parentheses.

The first set of Parentheses is group 1, the second is group 2, and so on.

Calling `group()` or `group(0)` returns the full matching string, `group(1)` returns group 1s matching string and so on.

Use `\(` and `\)` to match literal parentheses in the regex string.

The `|` pipe can match one of many possible groups.

`*` match 0 or more times

`?` match 0 or 1 times

`+` match 1 or more times

`{3}` will match the string 3 times `{3,5}` will match the string 3 to 5 times. Not inputting a number will make it so there is no minimum or maximum.

`{3,5}?` makes it a non-greedy match, it will only match the minimum if no question mark is used it will run a greedy match and will try to match the longest possible string.

You can create your own character class like `d` for digit or `w` for word charcaters or `s` for whitespace. Uppercase shorthand chracters matches all that are NOT digits, words or spaces.

You can use `[]` to make your own character clases `[^]` will make it a negative character class.

`.findall()` is similar to `.search()` but does not return a match object, it returns tuples with your matches.

`^` means the string must start with the pattern

`$` means the string must end with the pattern

`.` is a wildcard it matches anything except newlines

`re.compile(r'.*', re.DOTALL)` will also include newlines

`re.compile(r'[aeiou]', re.IGNORECASE)` will ignore case can also be shortened to `re.I`

`.sub()` acts as search and replace

```python
>>> namesRegex = re.compile(r'Agent (\w) \w*')
>>> namesRegex.finall('Agent Alice gave the secret documents to Agent Bob.')
['A', 'B']
>>> namesRegex.sub(r'Agent \1****', 'Agent Alice gave the secret documents to Agent Bob.')
'Agent A**** gave the secret documents to Agent B****.'
>>>
```

### Verbose Regular Expression

Allows you to make large regex more readable. For example:

```python
re.compile(r'''
(\d\d\d-)|     #Area Code
(\(\d\d\d) )   #-or- area code
\d\d\d         # first 3 digits
-              # second dash
\d\d\d\d       # last 4 digits
\sx\d{2,4}''', re.VERBOSE)
```
