---
id: d40r117bk5ij1tf5gamvchp
title: Files
desc: Python File Manipulation Notes
updated: 1647549345007
created: 1647539055031
---

## Filepaths and the OS Path Module

`os.chdir('filepath')` - allows you to change current working directory

`os.getcwd()` - gets current working directory

`os.listdir('c:\\folder1\\folder2\\')` - returns content of a directory

`os.makedirs('c:\\folder1\\folder2\\')` - creates new folders

`os.path.abspath()` - gets you the absolute path from a relative path

`os.path.isabs('filepath')` - returns true if the path in the params is absolute, false if not

`os.path.relpath('filepath1','filepath2')` - returns the relative path between two directories. 

`os.path.dirname('c:\\folder1\\folder2\\spam.png')` - returns the directory part of the filepath

`os.path.basename('c:\\folder1\\folder2\\spam.png')` - returns the filename and type part of a filepath

`os.path.exists('c:\\folder1\\folder2\\spam.png')` -returns bool if path exists or not

`os.path.isfile('c:\\folder1\\folder2\\spam.png')` - returns bool if filepath contains a file

`os.path.isdir('c:\\folder1\\folder2\\spam.png')` - returns bool if filepath is for a directory only

`os.path.getsize('c:\\folder1\\folder2\\spam.png')` - returns filesize in bytes

Example function to read filesize of all items in a folder

```python
totalSize = 0
for filename in os.listdir('c:\\folder1\\folder2\\'):
    if not os.path.isfile(os.path.join('c:\\folder1\\folder2\\', filename)):
        continue
    totalSize = totalSize + os.path.getsize(os.path.join('c:\\folder1\\folder2\\', filename))
```

## Plaintext Files

`.open('filepath', 'w' )` - second param can be 'a' for append, if not param is passed the file will be opened in readmode which will not allow you to write to it.

need to run `.close()` after any changes to the file for them to be saved

### Shelve Module

You can save variables in your Python programs to binary shelf files using the shelve module. This way, your program can restore data to variables from the hard drive.

```python
>>> import shelve
>>> shelfFile = shelve.open('mydata')
>>> cats = ['Zophie', 'Pooka', 'Simon']
>>> shelfFile['cats'] = cats
>>> shelfFile.close()
```

## Copying, Moving and Deleting

Copy a file
`shutil.copy('filepath1', 'filepath2')`

Copy all folder contents
`shutil.copytree('filepath1', 'filepath2')`

Move a file (or rename a file)
`shutil.move('filepath1', 'filepath2')`

Deleting files:

```python
>>> import os
>>> os.unlink('filepath') # delete a file
>>> os.rmdir('filepath') # delete a folder (must be empty)
>>> import shutil
>>> shutil.rmtree('filepath') #deletes a folder and its content
```

Note: send2trash is a pip module for not permanently deleting stuff.

## Walking the Directory Tree

```python
import os
for folderName, subfolders, filenames in os.walk('filepath'):
    print('The Folder is ' + folderName)
    print('The subfolders in ' + folderName + ' are: ' + str(subfolders))
    print('The filenames in ' + folderName + ' are: ' + str(filenames))
    print()
```
