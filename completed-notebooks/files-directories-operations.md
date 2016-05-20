# Session 3: Files and Directories Operations

In this session we provide an introduction into common operations with files and directories, like finding, copying, moving, deleting, renaming, etc.

We will use for this purpose a number of python modules included in the standard library:

- `os`
- `os.path`
- `shutil`
- `glob`
- `fnmatch`

These are the things we will learn today:

1. Working with directories, you will learn to...
	1. get the current working directory
	1. distinguish between relative and absolute paths
	1. compose a pathname
	1. list the content of a directory
	1. change the current directory
	1. create a directory
	1. copy a directory
	1. move a directory
	1. remove a directory
1. Working with files, you will learn to...
	1. get the path and the name of a file
	1. get the base name of a file and its extension
	1. copy a file
	1. move a file (rename)
	1. remove a file
1. Finding stuff, you will learn to...
	1. glob.glob
	1. fnmatch.fnmatch
	1. os.walk
	1. find all files matching a pattern
	1. find all directories matching a pattern
1. Miscellaneous, you will learn to...
	1. check if a pathname is a file or a directory
	1. check if a directory/file exists
	1. permissions

We have learnt so far how to read and write files.

```python
with open('README.md', 'r', encoding = 'utf-8') as infile:
    text = infile.read()
print(text)
```

So far, so good. But what if the file is not in the same directory as our script?

Then you need to indicate not only the name of the file, but its pathname. A pathname is a string indicating where a file or a directory is located within the file system.

## Working with directories

First we will need to import the appropriate modules:

```python
import os
```

### Where are we?

```python
# get current working directory
os.getcwd()
```

### Relative and absolute paths

There are two types of paths:

- relative (to the working directory)
- absolute (full and unique path to the file in your system, starts always with a `/`)

#### Example of relative path

```python
import os.path
# show it as relative path
os.path.relpath(os.getcwd())
```

#### Example of absolute path

```python
# get an absolute path
os.path.abspath('.')
```

Symbol | Meaning
---|---
`/` | ROOT directory
`~` | user home folder
`.` | current directory
`..` | one level up

Learn more about pathnames in UNIX at:

<http://teaching.idallen.com/cst8207/12f/notes/160_pathnames.html>

### Compose a pathname

If you have worked with Windows and Unix OS, you will have already noticed that paths are written following different conventions. Luckily, Python includes in its standard library the function `os.path.join()`. It help us to work with paths properly, no matter which OS we are using, by using the appropriate separator (`\` in Windows and `/` in Unix).

```python
os.path.join('wwc','resources','completed-notebooks')
```

`os.path.join` always yields a relative path to the current working directory.

### List the content of a directory

```python
os.listdir()
```

### Change the current directory

```python
a_relative_path = os.path.join('resources') # relative path
print(a_relative_path)
os.chdir(a_relative_path)
os.getcwd()
an_absolute_path = os.getcwd() # absolute path
print(an_absolute_path)
os.chdir(an_absolute_path)
os.getcwd()
```

### Challenges!

Change the working directory to the parent directory using the relative path symbols:

```python
os.chdir('..')
os.getcwd()
```

Change the working directory to the folder `completed-notebooks` which is inside `resources` using relative paths:

```python
os.chdir(os.path.join('resources','completed-notebooks'))
os.getcwd()
```

Change the working directory two levels up using relative path symbols:

```python
os.chdir(os.path.join('..','..'))
os.getcwd()
```

### Create a directory

```python
os.mkdir('test')
os.listdir()
a_deeper_path = os.path.join('tmp','test')
os.mkdir(a_deeper_path) # yields an error, intermediate folder missing
os.makedirs(a_deeper_path)
os.listdir()
```

### Copy a directory

```python
import shutil
shutil.copytree('tmp','tmp2')
os.listdir()
```

### Move a directory

```python
shutil.move('tmp2','..')
os.listdir()
os.listdir('..')
```

### Remove a directory

> **ACHTUNG!!!** There is no undo button, and no trash bin, so if you remove something, it will be lost **forever**.

```python
os.rmdir('test')
os.listdir()
os.rmdir('tmp') # yields an error, not empty
shutil.rmtree('tmp')
os.listdir()
shutil.rmtree(os.path.join('..','tmp2'))
os.listdir('..')
```

## Working with files

Working with files is very similar to working with directories. You will always need a pathname to indicate where the file is located.

```python
os.getcwd()
readme_path = os.path.join('..','README.md')
readme_path
readme_path = os.path.abspath(readme_path)
readme_path
```

### Get the path and the name of a file

```python
os.path.split(readme_path)
file_path, file_name = os.path.split(readme_path)
file_path
file_name
os.path.basename(readme_path)
```

### Get the base name of a file and its extension

```python
os.path.splitext(file_name)
file_basename, file_extension = os.path.splitext(file_name)
```

### Copy a file

```python
dst_folder = os.path.split(readme_path)[0]
dst_path = os.path.join(dst_folder,'README_copy.md')
shutil.copy(readme_path,dst_path)
os.listdir(dst_folder)
```

### Move a file (rename)

```python
new_dst_path = os.path.join(dst_folder,'README2.md')
shutil.move(dst_path,new_dst_path)
os.listdir(dst_folder)
shutil.move(new_dst_path,'.')
os.listdir(dst_folder)
os.listdir('.')
```

### Remove a file

> **ACHTUNG!!!** There is no undo button, and no trash bin, so if you remove something, it will be lost **forever**.

```python
os.remove('README2.md')
os.listdir()
```

## Finding stuff

We will need at least to building blocks to find files/directories:

- a function to check if the pathnames match a pattern or not.
- a function to go through the directory tree structure recursively.

### `glob.glob`

This function allows us to find pathnames matching a particular *glob* pattern, which is something similar to simple regular expressions. It returns a list of pathnames.

```python
import glob
md_files = glob.glob('*.md')
```

Be aware that its search is not recursive.

### `fnmatch.fnmatch`

Check if a file name (or the last element of a path) matches a *glob* pattern.

```python
import fnmatch
for file in os.listdir('.'):
    print(file, fnmatch.fnmatch(file,'*.md'))
```

The result is `True` or `False`.

A shortcut to filter those files/folders matching the pattern and saving them in a list is `fnmatch.filter`:

```python
fnmatch.filter(os.listdir('.'),'*resourc*')
fnmatch.filter(os.listdir('.'),'*.md')
```

### `os.walk`

This function goes through directory tree structure (a folder and its contents/subsfolders) creating a generator for all the elements. A generator is an iterable data structure (we can run loops on it), like a list. Each item in the generator is a tuple containing a string for the **path to the directory**, **a list of directories**, **a list of files**. This function finds everything.

```python
resources_contents = os.walk('resources')
for item in resources_contents:
    print(item)
```

### Find all files matching a pattern

```python
def get_file_pathnames(directory, pattern):
    matches = []
    for root, dirnames, filenames in os.walk(directory):
        for filename in fnmatch.filter(filenames, pattern):
            matches.append(os.path.join(root, filename))
    return matches

files = get_file_pathnames('.','*.md')
```

### Find all directories matching a pattern

```python
def get_dir_pathnames(directory, pattern):
    matches = []
    for root, dirnames, filenames in os.walk(directory):
        for dirname in fnmatch.filter(dirnames, pattern):
            matches.append(os.path.join(root, dirname))
    return matches

dirs = get_dir_pathnames('.','*.md')
```

## miscellaneous

### Check if a pathname is a file or a directory

```python
os.path.isdir('README.md')
os.path.isdir('resources')
os.path.isfile('resources')
os.path.isfile('README.md')
```

### Check if a pathname exists

```python
pathname_dir = os.path.join('resources','completed-notebooks')
os.path.exists(pathname_dir)
pathname_file = os.path.join(pathname_dir, 'nltk-session-1-complete.ipynb')
os.path.exists(pathname_file)
pathname_file = os.path.join(pathname_dir, 'nltk-session-10-complete.ipynb')
```

### Permissions

Permissions are properties assigned to directories or files stating who (which user or group of users) can do what (read, write, execute).

```python
file_info = os.stat('README2.md') # to know things about the file
# get the permissions
os.stat.filemode(file_info.st_mode)
# set the permissions
os.chmod('README2.md',0o664)
file_info = os.stat('README.md')
os.stat.filemode(file_info.st_mode)
```

## The challenge

### Find all completed notebooks in the repo

```python


```

### Create a folder inside `resources` called `backups`

```python


```

### Copy all completed notebooks into that folder

```python


```

### Change the working directory to the new folder

```python


```

### Rename all files by changing the extension to `.bkp`

```python


```

### Change the working directory to the root folder of the repo

```python


```

### Move the backups folder to the root

```python


```

### Delete the backups folder

```python


```

### Create a folder called `tmp`

```python


```

### Inside `tmp` create 100 copies of `README.md` prepending a prefix `copy1-` to each copy

```python


```

### Remove only files with an odd prefix (`copy1`, `copy3`, `copy5`)

```python


```

### Remove the `tmp` folder

```python


```

# Useful links and references

Official Python standard modules for file and directory access:

<https://docs.python.org/3.5/library/os.html#files-and-directories>

`os.path`

<https://docs.python.org/3.5/library/os.path.html?highlight=os.path>

Dive into Python 3:

<http://www.diveintopython3.net/comprehensions.html>

And final sections of:

<http://www.diveintopython3.net/files.html>

Tutorials point:

<http://www.tutorialspoint.com/python/python_files_io.htm>

Programiz:

<http://www.programiz.com/python-programming/directory>

Thomas-cokelaer:

<http://www.thomas-cokelaer.info/tutorials/python/module_os.html>

The future, `pathlib`:

<https://docs.python.org/3/library/pathlib.html>

<http://knowsuchagency.github.io/pyhi/posts/pathlib-and-ospath/>
