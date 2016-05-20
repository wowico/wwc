Witzelsucht Conditions
====

This warm-up session would be a little more theoretic than practical. It might seen a little abstract and you wonder why you need to know this. But let's try and see whether they help us charm the python =)

The end of the session will lead to Star Wars, I promise.

Fire up our https://try.jupyter.org/ notebook and let's go...


Built-ins and Keywords
====

Previously, we have discuss briefly the *"batteries included"* [built-in](https://docs.python.org/3.5/library/functions.html) functions in python. A very useful built-in function that will show us what a python object contains is `dir()`. So without importing anything, do a `dir()` in your ipython notebook at press `shift + enter`:

```python
dir()
```

You will see this:
 
```python
['__builtins__', '__doc__', '__name__', '__package__', 'keyword']
```

The `__builtins__` are the built-in functions that we have been discussing for the past two session. The underscores `__something__` notation is call the [double underscore (aka `dunder`)](https://wiki.python.org/moin/DunderAlias). 

 > *An awkward thing about programming in Python: there are lots of double underscores...My problem with the double underscore is that it's hard to say. How do you pronounce `__init__`?* - [Ned Batchelder](http://nedbatchelder.com/blog/200605.html#e20060522T162427)
 
 So if we do a dir on the dunder bulit-in:
 
 ```python
 dir(__builtin__)
 ```
 
We will see the (i) various types of Errors that can be caught by native python (we'll discuss about this later), (ii) many more dunders and (iii) built-in functions:

 ```python
 ['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException', 'BufferError', 'BytesWarning', 'DeprecationWarning', 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False', 'FloatingPointError', 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError', 'ImportWarning', 'IndentationError', 'IndexError', 'KeyError', 'KeyboardInterrupt', 'LookupError', 'MemoryError', 'NameError', 'None', 'NotImplemented', 'NotImplementedError', 'OSError', 'OverflowError', 'PendingDeprecationWarning', 'ReferenceError', 'RuntimeError', 'RuntimeWarning', 'StandardError', 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError', 'SystemExit', 'TabError', 'True', 'TypeError', 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError', 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning', 'ValueError', 'Warning', 'ZeroDivisionError', 
 '_', '__debug__', '__doc__', '__import__', '__name__', '__package__', 
 'abs', 'all', 'any', 'apply', 'basestring', 'bin', 'bool', 'buffer', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod', 'cmp', 'coerce', 'compile', 'complex', 'copyright', 'credits', 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'execfile', 'exit', 'file', 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int', 'intern', 'isinstance', 'issubclass', 'iter', 'len', 'license', 'list', 'locals', 'long', 'map', 'max', 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property', 'quit', 'range', 'raw_input', 'reduce', 'reload', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'unichr', 'unicode', 'vars', 'xrange', 'zip']
 ```
 
 And then we take a look at `keyword`:
 
 ```python
 print (dir(keyword))
 keyword.kwlist
 ```
 
 Now we see a list of familiar words we always type when coding in python. These are usually the highlighted words if you're using `ipython notebook` or a programming language sensitive editor:
 
 ```python
 print ( keyword.kwlist)
 ['and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'exec', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'not', 'or', 'pass', 'print', 'raise', 'return', 'try', 'while', 'with', 'yield']
 ```
 
You will realize that these are also the words that you cannot use as a variable to store a variable.
 

```python
# Usually we can call a variable anything we like.
this_variable = 'abc'
that_variable = 5
anything_we_like = 999
# But you cannot use a keyword as a variable
try = 123
```

You will see an error like this with `try = 123`:

```
  File "<stdin>", line 1
    try = 123
        ^
SyntaxError: invalid syntax
```
 
 ------
 
 **It's nice to know `dir()` and `keyword` and `builtin` but what are they useful for?**
 
  - Prevent yourself from reinventing the wheels, e.g. you don't need to write a sort algorithm, just use `sorted([5,1,3])`; see [this](http://stackoverflow.com/questions/13142347/how-to-remove-leading-and-trailing-zeros-in-a-string-python) for a very funny example of reinvent the wheels
  - `dir()` is a good source of information when you dig into code that is not yours and you want to see what is already coded, especially when you've no internet ;P
  - Some of these `keywords` and `builtins` have magic-like powers that you didn't know exist in python. Knowing more about them will surely save you lines of unnecessary code.
  - As linguists, ain't you curious about this pythonic language that keeps people so hooked up? Why do people go gaga over python? Does the programming language influence how we think and our culture? Is there a Sapir-Whorf phenomenon in python programmers? Why do people *come for the language and stay for the community*? The `builtins` and `keywords` says alot about python and its community =)
  
  
----

Condtions without Shampoo
=====

Now back to main topic of this *pywarmup*, conditions and iterations are the two most basic things in programming. Almost all programming languages builds software based on these two principles. 

**Conditions** refers to rules we write to disrupt/divert the sequential order of a python program. 

This example shows a sequential program where first we set ask the user to give value for `anumber` and then we double the number to get a new number (type the following code and press enter, another popup box will appear below and now you can key in the value):

```python
anumber = int(input('Enter a number:'))
newnumber = anumber * 2
print (newnumber)
```

Note that we use the `int()` type cast function to change the user input, this is because in `python3`, all user input collected using `input()` is by default of `str` type, so if we have a string, we can still do a mulitplcation but it will not be the desired numerical output we need, e.g.:

```python
# Multiplication of strings in python.
anumber = '2'
print (anumber * 2)
print (type(anumber * 2))
# Integer multiplication in python.
anumber = 2
print (anumber * 2)
print (type(anumber * 2))
```

Going back to the previous code, it was excuted sequentially from the first line to the second to the third. If we add a conditional line as such:

```python
anumber = int(input('Enter a number between 1-10:'))
if anumber < 11:
    newnumber = anumber * 2
else:
    newnumber = anumber * 4
print (newnumber)
```

Note that we use `anumber < 11` instead of `anumber < 10`, it's because of the inequality `anumber <= 10` would include 10 but `anumber < 10` won't.

Now we see that the code didn't go through all the lines but checks that `anumber < 11` and double the number without tripling it after the `else` line. **What if we want to check if the `number < 6`?**:

```python
anumber = int(input('Enter a number between 1-5:'))
if anumber < 11:
    newnumber = anumber * 2
if anumber < 6:
    newnumber = anumber * 3
else:
    newnumber = anumber * 4
print (newnumber)
```

Gotcha if you expect the number to only multiply by 2 or 3 or 4, **then you're wrong**. It multiplied by 2 then multiply by 3, it's because the multiple ifs are sequential. 

To group multiple conditions into a single block, you can use `elif`, e.g.:

```python
anumber = int(input('Enter a number between 1-5:'))
if anumber < 11:
    newnumber = anumber * 2
elif anumber < 6:
    newnumber = anumber * 3
else:
    newnumber = anumber * 4
print (newnumber)
```

Gotcha again! If you expect the number to multiple by 3, **then you're wrong**. It checks for the first condition that is valid and then skips to the end of the if-elif-else block and prints the `newnumber`:

You can put even more `elif` but only the first valid conditions will be considered, e.g.:

```python
anumber = int(input('Enter a number between 1-5:'))
if anumber < 11:
    newnumber = anumber * 2
elif anumber < 6:
    newnumber = anumber * 3
elif anumber > 1:
    newnumber = anumber * 9
elif anumber > 2:
    newnumber = anumber * 5
else:
    newnumber = anumber * 4
print (newnumber)
```

And to combine multiple conditions, you can also use the `and` keyword and/or the `or` keyword, you can also check for equivalence with the `is` and `not` keywords:

```python
anumber = int(input('Enter a number between 2-5:'))
if anumber < 6 and anumber > 1:
    newnumber = anumber * 2
elif anumber is 2 or anumber is not 5:
    newnumber = anumber * 3
else:
    newnumber = anumber * 4
print (newnumber)
```

Play around the conditions with different inputs and add your own conditions and see what you get as output after you `shift + enter`. You shall be enlightened by some quirks of python conditions. 

Do note that all conditions without the `if-elif-else` keywords are a boolean, i.e. they are either `True` or `False`, also parenthesis like in math works the same in python conditions, e.g.:

```python
a = 3
print(3 > 2)
print(2 is True) # Returns False because 2 is a number and True is a boolean.
print((3 > 2) is True) # Returns True because `(3>2)` returns a True and `True is True`
```

These conditions goes beyond numerical comparisons, in python one can check for string conditions, sometimes even strange boolean conditions. But we will go through all that in the later sessions. For a taster:

``` python
# Quirky but nice string comparisons
astring = 'a'
bstring = 'b'
if astring < bstring:
    print('what? can a character be compared?')

# Caps vs no caps
astring = 'a'
acapstr = 'A'
if astring == acapstr:
    print('ain't they the same?')
else:
    print ('same same but different')

# Nully strings.
astring = ''
if astring is not '': 
    print('This checks for whether astring is not an empty string.)

if astring: # It's the same expression as the above but shorter.
    print('This checks for whether astring is not an empty string.)
```

----

Congratualations!!!
====

This is a tough warmup session and now you have learnt more about `builtins`, some basics of the `keywords` and quite a lot of quirky python conditions!!

**As promised**: *Read up on [Yoda conditions](https://en.wikipedia.org/wiki/Yoda_conditions), you must*.
