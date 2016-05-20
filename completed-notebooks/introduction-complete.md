# Session 1: Orientation

Welcome to *Jupyter*. Through this interface, you'll be learning a lot of things:

* A Programming language: **Python**
* A Python library: **NLTK**
* Overlapping research areas: **Corpus linguistics**, **Natural language processing**, **Distant reading**
* Additional skills: **Regular Expressions**, some **Shell commands**, and **tips on managing your data**

You can head [here](https://github.com/interrogator/wwc) for the fully articulated overview of the course, but we'll almost always stay within this **Jupyter** interface.

Remember, everything we cover here will remain available to you after we're through is over, including a completed version of these notebooks. It's all accessible via [GitHub](https://github.com/interrogator/wwc).

**Any questions before we begin?**

Alright, we're off!

## Text as data

Programming languages like Python are great for processing data. In order to apply it to *text*, we need to think about our text as data. This means being aware of how text is structured, what extra information might be encoded in it, and how to manage to give the best results.

## What is the Natural Language Toolkit?

We'll be covering some of the theory behind corpus linguistics later on, but let's start by looking at some of the tasks NLTK can help you with.

NLTK is a Python Library for working with written language data. It is free and extensively documented. Many areas we'll be covering are treated in more detail in the NLTK Book, available free online from [here](http://www.nltk.org/book/). 

> Note: NLTK provides tools for tasks ranging from very simple (counting words in a text) to very complex (writing and training parsers, etc.). Many advanced tasks are beyond the scope of this course, but by the time we're done, you should understand Python and NLTK well enough to perform these tasks on your own!

We will start by importing NLTK, setting a path to NLTK resources, and downloading some additional stuff.

```python
import nltk # Use for importing the nltk library

user_nltk_dir = "/home/researcher/nltk_data" # Specify our data directory
if user_nltk_dir not in nltk.data.path: # Make sure nltk can access this dir.
    nltk.data.path.insert(0, user_nltk_dir)
nltk.download("book", download_dir=user_nltk_dir, quiet=True) # Download book materials to data dir
```

Oh, we've got to import some corpora used in the book as well...

```python
from nltk.book import *  # asterisk means 'everything'
```

Importing the book has assigned variable names to ten corpora. We can call these
names easily:

```python
#text1
text2
#text3
```

Additionally, their first sentences have been predefined:

```python
#sent7
sent8
#sent9
```

... notice how even without any real context, we can understand what a corpus might contain. Though people often accuse quantitative/corpus linguists of removing language from context, people forget that in large part, **context is embedded in the lexicogrammar of texts**.

### Exploring vocabulary

NLTK makes it really easy to get basic information about the size of a text and the complexity of its vocabulary.

`len()` gives the number of symbols or 'tokens' in your text. This is the total number of words and items of punctuation.

`set()` gives you a list of all the tokens in the text, without the duplicates.

Hence, `len(set(text3))` will give you the total number unique tokens. Remember this still includes punctuation.

`sorted()` places items in the list into alphabetical order, with punctuation symbols and capitalised words first.

```python
len(text3)
```

```python
len(set(text3))
```

```python
sorted(set(text3)) 
```

We can investigate the *lexical richness* of a text. For example, by dividing the total number of words by the number of unique words, we can see the average number of times each word is used.

We can also count the number of times a word is used and calculate what percentage of the text it represents.

```python
len(text3)/len(set(text3))
```

```python
text4.count("American")
```

**Challenge!**

How would you calculate the percentage of Text 4 that is taken up by the word "America"?

```python
100.0*text4.count("America")/len(text4) 
```

### Exploring text - concordances, similar contexts, dispersion

`concordance()` shows you a word in context and is useful if you want to be able to discuss the ways in which a word is used in a text. 'Similar' will find words used in similar contexts; remember it is not looking for synonyms, although the results may include synonyms.

```python
text1.concordance("monstrous")
```

```python
text1.similar("monstrous")
```

```python
text2.similar("monstrous")
```

```python
text2.common_contexts(["monstrous", "very"])  # this function takes two arguments
```

Python also lets you create graphs to display data. To represent information about a text graphically, import the Python library *numpy*. We can then generate a dispersion plot that shows where given words occur in a text.

```python
%matplotlib inline
import numpy
text1.dispersion_plot(["whale"])
```

### Challenge! ###

Create a dispersion plot for the terms "citizens", "democracy", "freedom", "duties" and "America" in the innaugural address corpus. What do you think it tells you?

```python
text4.dispersion_plot(["citizens", "democracy", "freedom", "duties", "America"]) # plot five words longitudinally
```

## How Python works

We've seen a bit now of how NLTK can help you to interrogate a text. Let's back up and talk about Python itself and the environment we're using.

```python
# A simple welcome message printer.
# Anything after a hash is ignored
# Run a cell with shift+enter

condition = True
if condition is True:
    print('Welcome to Python and Jupyter.')
```

## Jupyter

Before we start coding, we should familiarise ourselves with the *Jupyter* interface. Click `Help --\> User interface tour` to begin. 

> Keyboard shortcuts come in very handy. Click `Help --\> Keyboard shortcuts` to get an overview. *The more you code, the less you'll want to use your mouse*!

## Python: core concepts

If you're new to Python, there are a few core concepts that will help you understand how everything works. Here, we'll cover:

* Significant whitespace
* Input/output types
* Commands and arguments
* Defining functions
* Importing libraries, functions, etc.

### Significant Whitespace

One thing that makes Python unique is that whitespace at the start of the line (use four spaces for consistency!) is meaningful. In many other languages, whitespace at the start of lines is simply a readability convention.

```python
# Fix this whitespace problem!

string = 'user'
if string == 'user':
print('Phew, fixed.')
```

So, whitespace tells both Python and human readers where things start and stop.

### Input/Output Types

* Python understands different *types* of input, including *string*, *unicode string*, *integer*, *item*, *tuple* and *dict*.
* Different types of information behave in different ways, and the ways they are represented visually are different as well.
* You should always be aware of what kind of type you're passing around, and what is the most appropriate for your data
* For example, if you're trying to do maths, you'll want to be working with *integers* and/or *floats*:

```python
1 + 2  # integer plus integer
1 + 2.0 # integer plus float
```

```python
1 + '2'  # integer plus string
```

Note the error message. These will help you to understand what went wrong. The first part looks like gobbledygook to a new user, but the rest is helpful for us. Line 3 of error tells us what command was executing when the error happened, which can assist in isolating a problem.

The leading digit is the line number. Line 4 actually tells us what the error was - that's what we probably would have googled if we were looking for a solution.

You can determine the type of data stored in a variable with *type()*. Here are some of the most common types. Note how quotation marks, and brackets are used to distinguish between them when writing code.

```python
datum = 'A string'
print(type(datum))
datum = u'A unicode string'
print(type(datum))
datum = 42
print(type(datum)
datum = ['item']
print(type(datum))
datum = ('item', 'another')
print(type(datum))
datum = {'entry': 7}
print(type(datum))
```

Sometimes you can sometimes easily convert between types.

```python
num = '2'
1 + int(num)
```

... and sometimes it's not so easy:

```python
adj = ['wicked', 'radical', 'awesome']
more_adj = str(adj) + 'overwhelmed'
print(more_adj)
```

Anybody care to explain what just happened?

### Basic syntax

**Only do this section if we have time!!**

Python has *variables* and *commands*. Commands may have *arguments* and
*options*.

> *Jupyter* highlights your code automatically, which can help you read it faster
and spot problems.

```python
from math import sqrt  # importing math library and square root function
avariable = 50  # make a variable that is 50 as integer
answer = sqrt(avariable)  # figure out the answer by issuing a command with avariable as an argument
answer  # tell us
```

```python
# This example has two arguments
from math import pow  # importing pow function (pow is short for 'power')
avariable = 50
answer = pow(avariable, 3)  # 50 to the power of 3
answer
```

## Advantages of Jupyter

So, we've been writing Python code in this [Jupyter](http://jupyter.org/) interface. Why?

* The main strength of Jupyter is that you can run bits of code individually, so you don't have to keep repeating things. For example, if you scroll up to the last function and replace the 50 with 2, you can re-run that code and get the new answer.
* Here, we can also display images alongside code, and to save the input and output together.
* Jupyter makes learning a bit easier, as mistakes are easier to find and do not break an entire workflow.
* This interface allows use to use Python and IPython, as well 40+ other languages.

You can get more information on IPython, including how to install it on your own machine, at the [Jupyter Homepage](http://jupyter.org/). Complete documentation is [here](http://jupyter.readthedocs.org/en/latest/index.html).

So, at this point, why don't you tell us what you make of it all. Can anyone see potential for Python/Jupyter in their own research? What are you working on, anyway?

Anything you're struggling with so far?

At this point, we want to dive more deeply into general Python functionality. We want to define some functions, manipulate some lists, and understand better what variables are and what they do.

### Defining a function

Next, we'll talk about *functions*. Here's an example:

```python
def welcomer(name):
    print('Welcome ' + name + '!')
```

Notice that it doesn't do anything by itself. It needs to actually be *called*, and given some data:

```python
welcomer('Kim')
```

You may wish to repeat an operation multiple times looking at different texts or different terms within a text. Instead of re-entering the formula every time, you can assign a name and set of actions to a particular task.

Previously, we calculated the lexical diversity of a text. In NLTK, we can create a function called **lexical diversity** that runs a single line of code. We can then call this function to quickly determine the lexical density of a corpus or subcorpus.

Advantages of functions:

1. Save you typing
2. You can be sure you're doing exactly the same operation every time
3. When there's a problem in your code, you can fix the problematic function without causing a chain reaction

> Learn to love tab-completion! Typing the first one or two letters of a command you've used previously then hitting tab will auto-complete that command, saving you typing (i.e. time and mistakes!).

### Challenge!

Using a function, determine which of the nine texts in the NLTK Book has the highest lexical diversity score.

```python
def lexical_diversity(text):
    return len(text)/len(set(text))
```

```python
#After the function has been defined, we can run it:
lexical_diversity(text2)
```

The parentheses are important here as they sepatate the the task, that is the work of the function, from the data that the function is to be performed on.

The data in parentheses is called the argument of the function. When we use a function, we say that we 'call' it.

Other functions that we've used already include `len()` and `sorted()` - these were predefined. `lexical_diversity()` is one we set up ourselves; note that it's conventional to put a set of parentheses after a function, to make it clear what we're talking about.

### Lists

Python treats a text as a long list of words. First, we'll make some lists of our own, to give you an idea of how a list behaves.

```python
sent1 = ['Call', 'me', 'Ishmael', '.']
```

```python
sent1
```

```python
len(sent1)
```

The opening sentences of each of our texts have been pre-defined for you. You can inspect them by typing in `sent2` etc.

You can add lists together, creating a new list containing all the items from both lists. You can do this by typing out the two lists or you can add two or more pre-defined lists. This is called *concatenation*.

```python
sent4 + sent1
```

We can also add an item to the end of a list by appending. When we `append()`, the list itself is updated.

```python
sent1.append('Please')
sent1
```

There are some things we can do to make it easier to read the contents of a string. Note that we get some brackets and so on when we try to print the items in a list as a string.

```python
salad = []  # declare an empty list
salad.append('apple')  # add apple
salad.append('orange')  # add orange
print('Our fruit salad contains: ' + str(salad))
```

If we want to print our ingredients in a nicer looking form, we might use a function like `join()`.

```python
salad = []
salad.append('apple')
salad.append('orange')
listasastring = ''.join(salad)  # create a string with all the list items joined together
print('Our fruit salad contains: ' + listasastring)
```

... whoops! Still ugly. We didn't put anything in between the '' to use as a delimiter.

```python
fruitsalad.append('canteloupe')
listasastring = ', '.join(fruitsalad)  # note the comma and space in quotation marks
print('Our fruit salad contains: ' + listasastring)
```

###  Indexing Lists

We can navigate this list with the help of indexes. Just as we can find out the number of times a word occurs in a text, we can also find where a word first occurs. We can navigate to different points in a text without restriction, so long as we can describe where we want to be.

```python
text4.index('awaken')
```

This works in reverse as well. We can ask Python to locate the 159th item in our list (note that we use square brackets here, not parentheses). **Python, unlike some other languages, starts counting at zero**.

```python
text4[158]
```

As well as pulling out individual items from a list, indexes can be used to pull out selections of text from a large corpus to inspect. We call this *slicing*:

```python
text5[16715:16735]
```

If we're asking for the beginning or end of a text, we can leave out the first or second number. For instance, `[:5]` will give us the first five items in a list while `[8:]` will give us all the elements from the eighth to the end.

```python
text2[:10]
```

```python
text4[145700:]
```

To help you understand how indexes work, let's create one.

We start by defining the name of our index and then add the items. You probably won't do this in your own work, but you may want to manipulate an index in other ways. Pay attention to the quote marks and commas when you create your test sentence.

```python
sent = ['The', 'quick', 'brown', 'fox']
sent[0]
print(sent[2])
```

It's quite annoying, writing out lists though. Python has some simple methods for helping us out here:

```python
sent = 'The quick brown fox'
sent = sent.split()
sent
```

Note that the first element in the list is zero. This is because we are telling Python to go zero steps forward in the list. If we use an index that is too large (that is, we ask for something that doesn't exist), we'll get an error.

We can modify elements in a list by assigning new data to one of its index values. We can also replace a slice with new material.

```python
sent[2] = 'furry'
sent[3] = 'child'
sent
```

###  Defining variables

In Python, we give the items we're working with names, a process called assignment. For instance, in the NLTK corpus, 'Sense and Sensibility' has been assigned the name 'text2', which is much easier to work with.

We also assigend the name 'sent' to the sentence that we created in the previous exercise, so that we could then instruct Python to do various things with it. Assigning a variable in python looks like this:

    variable = expression

You can call your variables (almost) anything you like, but it's a good idea to pick names that will be meaningful and easy to type. You can't use words that already have a meaning in Python, such as import, def, or not. If you try to use a word that is reserved, you'll get a syntax error.

### Challenge

* Write out a sentence
* Split it into a list of tokens
* Print the first five tokens
* Print the the tokens, sorted alphabetically

```python
firstline = 'It was a dark and stormy night ; the rain fell in torrents'
opening = firstline.split()
clause = opening[0:7]
alphabetised = sorted(clause)
```

Note that assigning a variable just causes Python to remember that information without generating any output.

If you want Python to show you the result, you have to ask for it (this is a good thing when you assign a variable to a very long list!).

```python
print(clause)
```

```python
print(alphabetised)
```

### Frequency distributions

We can use Python's ability to perform statistical analysis of data to do further exploration of vocabulary. For instance, we might want to be able to find the most common or least common words in a text. We'll start by looking at frequency distribution.

```python
from collections import Counter
counted = Counter(text1)
```

The output here is a *dict*, with *keys* and *values*.

```python
counted.keys()[:5]
```

We can look things up in a *dict* like so:

```python
counted['whale']
```

This kind of dictionary also has a special method, where we can access the items with the highest values:

```python
counted.most_common(50)
```

We now have some plottable data. We can use *pandas* to do this. It's a module for manipulating data structures, like R. It's really awesome.

```python
import pandas
data = pandas.DataFrame(counted.values(), index = counted.keys(), columns = ['Occurrences'])
data
```

We can sort by frequency:

```python
# sort by the occurrences column, reversed
data = data.sort('Occurrences', ascending = False)
data
```

... And now plot!

```python
data[:10].plot()
data[:10].plot(kind = 'bar')
```

... powerful, eh?

### Loops

One of the most powerful things about programming is the ability to loop through data and perform the same action over and over again. When writing loops in Python, indentation is necessary again:

```python
for word in sent5:
    print('Word: ' + word.upper())
```

### Challenge!

**Create a function called `common_words()`, which prints the 15 most common words in an NLTK text.**. If that's easy for you:

* Add a keyword argument that controls how many entries to print
* Format the output nicely
* Ignore punctuation

```python
def common_words(text):
    counted = Counter(text)
    print(counted.most_common(15))
```

```python
def common_words(text, n = 15):
    """for experts!"""
    counted = Counter([w for w in text if w.isalnum()])
    for word, count in counted.most_common(n):
        print(word)
```

... what have we learned about language from this?

### Counting word lengths

As well as counting individual words, we can count other features of vocabulary, such as how often words of different lengths occur. We do this by putting together some things we've already learned

```python
lengs = Counter()
for token in text1:
    lengs[len(token)] += 1
lengs
```

We can get the most common result easily:

```python
lengs.most_common(1)
```

... and of course, we can plot our data. Do you remember how?

```python
data = pandas.DataFrame(lengs.values(), index = lengs.keys(), columns = ['Word length'])
data.plot(kind = 'pie')
```

```python
data['Word length'].plot(kind = 'pie')
```

We might be interested in using this kind of technique to find very long words in our text:

```python
v = set(text4)
long_words = []
for word in v:
    if len(word) > 15:
        if word.lower() not in long_words:
            long_words.append(word.lower())
sorted(long_words)
```

### Challenge! ###

Can you find all the words in a text that are more than seven letters long and occur more than seven times? Advanced folk, use list comprehension, and do it in as few characters as possible.

```python
results = []
for token in text5:
    if len(token) > 7:
        if text5.count(token) > 7:
            if token not in results:
                results.append(token)
results
```

```python
# expert mode!
set(w for w in text5 if len(w) > 7 and text5.count(w) > 7)
```

```python
#
```

```python
#
```

```python
#
```

```python
#
```

```python
#
```

### Test-driven programming

In test-driven design, you define your expected output, and then write code that achieves that. This makes it easy to keep track of your progress, and prevents *feature creep*.

For the last part of the session, explore some NLTK texts, using some of Python's *operators*, listed below.

### Common relationals

|  Relational | Meaning |
|--------------:|:------------|
| <    |  less than |
| <=   |   less than or equal to |
| ==  |    equal to (note this is two "=" signs, not one) |
| !=   |   not equal to |
| \>   |   greater than |
| \>= |   greater than or equal to |

### Common operators

| Operator  | Purpose  |
|-----------|------------|
| s.startswith(t) | test if s starts with t |
| s.endswith(t)  |  test if s ends with t |
| t in s         |  test if t is a substring of s |
| s.islower()    |  test if s contains cased characters and all are lowercase |
| s.isupper()    |  test if s contains cased characters and all are uppercase |
| s.isalpha()    |  test if s is non-empty and all characters in s are alphabetic |
| s.isalnum()    |  test if s is non-empty and all characters in s are alphanumeric |
| s.isdigit()    |  test if s is non-empty and all characters in s are digits |
| s.istitle()    |  test if s contains cased characters and is titlecased (i.e. all words in s have initial capitals) |

```python
#
```

```python
#
```

```python
#
```

### Bonus!

You'll remember right at the beginning we started looking at the size of the vocabulary of a text, but there were two problems with the results we got from using:

     len(set(text1))


This count includes items of punctuation and treats capitalised and non-capitalised words as different things (*This* vs *this*). We can now fix these problems. We start by getting rid of capitalised words, then we get rid of the punctuation and numbers.

```python
toks = []
for token in text1:
    if token.isalnum():
        toks.append(token.lower())
len(set(toks))

# or, on one line:
# len(set(token.lower() for token in text1 if token.isalnum()))
```

### Congratulations!

You've now had a really great peek into how computers understand written text. In the next session, we'll have all the foundations we need to do some common corpus linguistic tasks, like collocation, keywording and n-gramming.
