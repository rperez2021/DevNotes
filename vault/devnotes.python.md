---
id: THqFYHlDTguT4tBejc3TH
title: Python
desc: Python Notes
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

## Excel in Python

Module OpenPyXL handles .xlsx files, the command openpyxl.load_workbook(filepath) returns a Workbook object.

`get_sheet_names()` and `get_sheet_by_name()` will get you a Worksheet object.

`sheet[A1]` will get you Cell Objects

`sheet[A1],value == "Purple"`

## PDF in Python

```python
import PyPDF2 # is the module recommended
pdfFile = open(filepath, 'rb')  # to open PDF
reader = PyPDF2.PdfFileReader(pdfFile) # to read PDF in PyPDF2
reader.numPages # returns number of pages in PDF
reader.getPage(0) # gets a page
reader.extractText()
for pageNum in range(reader.numPages):
    print(reader.getPage(pageNum).extractText())
```

`PdfFileWrite()` is the command to write a new PDF

### Word in Python

`python-docx`

```python
pip install python-docx
import docx
d = docx.Document(filepath)
d.paragraphs # returns a list with all the objects in a docx
d.paragraphs[0] #returns a paragraph object from the list
d.paragraphs[0].text # returns the text within a single object in the list
p.runs # returns a list of all the run objects
p.runs[0].text # returns the text in the run object
p.runs[0].bold # returns true if the run object is bold returns "NONE" (not false) if its not, this works for italic, bold and underline
```

Word documents contain paragraph and run objects for structure.

A run is created every time there is a style change in the text of a document. So italics, bold, and underline.
