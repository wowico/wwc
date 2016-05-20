## Warming Up to Python

This notebook is for anyone new to the Python language. If fluent Parseltongue (Python) coder, move on to the next notebook. Otherwise, let's go...

Go to this https://try.jupyter.org/ , click on **new** -> **Python 3**  and it will bring you to a next page. [see this if you can't find the button to start the notebook](http://ibin.co/2MqL1JAmPqKg)

This is the Jupyter notebook (aka `ipython-notebook`) interface, every "clickable" box is refer to as a cell. And you can switch between a text cell, where you can write text like this or a code cell where you can execute python code on the fly. To proceed, click on each code cell and press `shift + enter`...

## Hello World!

Like all the programmers that came before us, let's try to make the computer print "Hello World" in `python`:

```python
print ("Hello Word")
```

The philosophy of the python language is to write readable code, executing the following line in python would describe the **Zen of Python**:

```python
import this
```

And the simplicity extends to dealing with numbers:

```python
print(3 + 5)
```

We can also save these strings or numbers and then use them later on by saving them into variables:

```python
x = "Hello World"
y = 3 + 5
z = x + ", Welcome to the matrix"
print(z)
yy = y + y
print(yy)
```

Computers are not as smart as the humans who created them. They don't know strings, integers, numbers, text or any sort of types. We, as humans, have to specifically tell them. And in the case of python, when we create a string/text object, python assumes that anything embedded between quotation marks as strings and tell the computer that the thing we are telling the computer is a string.

We can know the type of a variable in python using one of the [built-in functions](https://docs.python.org/2/library/functions.html) `type()`:

```python
x = "Hello World"
type(x)
```

## Parseltongue Baby Talk

Here's some intuitive ways to manipulate text, numbers, lists in python using some built-in functions.

This is how one would define a list of things in python:

```python
list1 = [1,1,2,2,3,4,5,6,6]
```

And you can simply count the number of items in the list with `len()`:

```python
len(list1)
```

You can also "extract" the number of **unique** items in the list by transforming the list into a set:

```python
set(list1)
```

The term to call this kind of transformation is called, "*type casting*". To reiterate the point, let's see how one can check the *types*:


```python
a = [1,1,2,2,3,4,5,6,6]
print(type(a), len(a))
b = set(a)
print(type(b), len(b))
```

We can also remove items from a list by iterating through each item and checking them. So, let's say we don't want twos and sixes in our list:


```python
a = [1,1,2,2,3,4,5,6,6]
alist_with_no_2s_and_no_6s = [num for num in a if (num is not 2) and (num is not 6)]
print(alist_with_no_2s_and_no_6s)
```

You can also check if the item is in a list of unwanted items, e.g.:

```python
a = [1,1,2,2,3,4,5,6,6]
alist_with_no_2s_and_no_6s = [num for num in a if num not in (2,6)]
print(alist_with_no_2s_and_no_6s)
```



## Pythonic Slices (not Pizza)

To access a particular subset of a list, one should access the subset using [slices](https://docs.python.org/2/tutorial/introduction.html):

```python
a = [1,1,2,2,3,4,5,6,6]

first_three_items = a[:3]
print(first_three_items)

last_three_items = a[-3:]
print(last_three_items)
```

One could also explicitly state the starting/ending indices when access a python slice, so the follow code would achieve identical output as the code above:

```python
a = [1,1,2,2,3,4,5,6,6]
num_items_in_a = len(a)

first_three_items = a[0:3]
print(first_three_items)

last_three_items = a[-3:len(a)]
print(last_three_items)
```

Note that the indices in python starts from 0. So to access the first item in a list:

```python
a = [1,1,2,2,3,4,5,6,6]
first_item = a[0:1]
print(first_item)
```

Similarly a string is a list of characters and we can access substrings with slices (Note that even spaces are characters):

```python
sentence = "I am working with corpora"
first_three_chars = sentence[:3]
print(first_three_chars)
last_three_chars = sentence[-3:]
print(last_three_chars)
```

A picture tells a thousand words, I hope the following picture clearly explains what python slices do:

![Python Slices](http://infohost.nmt.edu/tcc/help/pubs/python/web/fig/slicing.png)

----

Strings are particularly easy to manipulate in python and that is the primary reason many researchers use python to *work with corpora*

You can sound angry by uppercasing every letter or lower case everything is you like to soften the tone ;P:

```python
sentence = "I am working with corpora"
print(sentence.upper())
print(sentence.lower())
```

Or you could check whether a character is upper or lower case:

```python
word_i = "I"
word_i.isupper() # Returns true if `word_i` is uppercase.
```

Now you try and see how to check if `word_i` is lowercase (fill in your own code in place of ?????)

```python
word_i = "I"
word_i.is?????()
```

"One of the best qualities of Python is its consistency. After working with Python for a while, you are able to start making informed, correct guesses about features that are new to you." - [Fluent Python by Luciano Ramalho](http://shop.oreilly.com/product/0636920032519.do)

## More Pythonic idioms when dealing with strings

**Counting the no. of character in a sentence**

```python
sentence = "I am working with corpora"
print (len(sentence))
```

**Counting the no. of words in a sentence**

```python
sentence = "I am working with corpora"
tokens = sentence.split()
print(len(tokens))
```

**Getting the index of the first instance of a word in a sentence**

```python
sentence = "I am working with corpora"
tokens = sentence.split()
print(tokens.index('am'))
```

**Slicing sentence up**

```python
sentence = "I am working with corpora"
tokens = sentence.split()
first_three_words = tokens[:3]
last_three_words = tokens[-3:]
print(first_three_words)
print(last_three_words)
```

(We'll see more of these when we deal with Ngrams in the future)

**Removing stop words**

Similar to how we remove unwanted items in a list of integers, we do the same with a list of strings:

```python
sentence = "I am working with corpora"
tokens = sentence.split()
stopwords = ['I', 'am', 'with]
tokens_no_stop_words = [word for word in tokens if word not in stopwords]
print(tokens_no_stop_words)
```

(The `[word for word in tokens if word not in stopwords]` code is sort of a funny syntax, it's call **list comprehension** and we'll explain it in the later sessions.)

## Jupyter/IPython Notebook Tricks

Now, for some Jupyter/Ipython Notebook tricks that one would find useful.

If you want something to be "silenced" as you write multiple lines of code, you can use this the `clear_output()` function. For example, let's say you have a function that sums 2 integers and it always prints this annoying message that says, "Summing Integers...".

```python
def sum_int(x, y):
    print("Summing Intergers...")
    return x + y

z1 = sum_int(3, 5)
z2 = sum_int(2, 2)
```

*Imagine if you have to call that function 1 million times...*

To silence that message in a function, you can do this:

```python
from IPython.display import display, clear_output 

def sum_int(x, y):
    print("Summing Intergers...")
    return x + y

z1 = sum_int(3, 5)
z2 = sum_int(2, 2)
clear_output()
```

**Voila, no annoying messages!!**

Alright that's all the warm-up there is for today's WwC!!! stay-tuned for the next pythonic warm-up...
