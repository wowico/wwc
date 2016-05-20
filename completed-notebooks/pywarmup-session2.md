Warming Up to Python
====

*"To warm up, pythons find sunny places and adopt positions that maximise their exposure"* - [Wikipedia](https://en.wikipedia.org/wiki/Ectotherm#Adaptations)

To follow up on our [first warm up session](https://github.com/interrogator/wwc/blob/master/resources/completed-notebooks/pywarmup-session1.md), we will go through some pythonic container types that are pretty neat.

So let's fire up the https://try.jupyter.org/ notebook and let's go...


Build up on Built-ins
====

Python comes with *"batteries included"*, we have introduced some [built-in](https://docs.python.org/2/library/functions.html) functions that in the previous warm-up session:

```python
list1 = [6,1,2,7,3,4,2,6,3]
print(list1) # Prints the variable *list1* to the console
len(list1)   # Get the length/size of the variable *list1*
set(list1)   # Creates a set with the variable *list1*
type(list1)  # Shows the type for the variable *list1*
```

Here's a few more built-ins that one would commonly use when interacting with a list of numbers:

```python
list1 = [6,1,2,7,3,4,2,6,3]
max(list1)
min(list1)
sum(list1)
sorted(list1)
```

Once again, we see that the function naming in python is intuitive and without even looking at the outputs of the built-in functions above, we know what the function does. *"Explicit is better than implicit"* - [The Zen of Python](https://www.python.org/dev/peps/pep-0020/).

**But how many built-ins are there in python?** 76 , see https://docs.python.org/2/library/functions.html

We'll see more of them in the later sessions

Comprehending List with List Comprehension
====

Given a list we learn how to use a `for` loop to iterate through the elements inside the list one by one, e.g.

```python
list1 = [6,1,2,7,3,4,2,6,3]
for num in list1:
    if num < 5:
        print(num)
```

And to extend a list we can do this:

```python
list1 = [6,1,2,7,3,4,2,6,3]
new_num = 100
list1.append(new_num)
print(list1)
```

The append function adds the new number at the end of the list. To insert an element into a specified position into a list:

```python
list1 = [6,1,2,7,3,4,2,6,3]
new_num = 100
# Adds to *new_num* to the 6th element in the list
list1.insert(5, new_num) # Note that in a list indexing it goes from 0, 1, 2, 3, ...
```

So naturally to add an element to the start of the list (aka. prepend), we do:

```python
list1 = [6,1,2,7,3,4,2,6,3]
new_num = 100
list1.insert(0, new_num)
```

Going back to the first `for` loop example where we print out the elements when it's smaller than 5. If we want to keep track of these numbers lower than 5, we can keep all these element in a new list:

```python
list_lower_than_5 = []
list1 = [6,1,2,7,3,4,2,6,3]
for num in list1:
    if num < 5:
        list_lower_than_5.append(num)
print (list_lower_than_5)
```

But instead of doing it in the 4-5 lines, we can simply use [**list comprehension**](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions) to achieve the same filtered list. 

```python
list1 = [6,1,2,7,3,4,2,6,3]
list_lower_than_5 = [num for num in list1 if num < 5]
print (list_lower_than_5)
```

Dear Dictionary 
====

Dictionary is a data type in python like the list it is a "**container**" data type. There are four basic container data types in python, `list`, `set`, `dict` and `tuple`. Instead having one item in each slot for the container, a dictionary has a key-value pair for each slot in the container.

Let's try to count word occurence in a sentence.

```python
sent = 'the quick brown fox jumps over the lazy dog'.split()
word_counter = {} # the curly brackets is how you would initialize a dict.
word_counter['the'] = sent.count(the) # Add to the dict a key-value pair (the word 'the' and its count)
word_counter
```

Now let's iterate through the sentence and add each word and their counts to the `word_counter`:

```python
sent = 'the quick brown fox jumps over the lazy dog'.split()
word_counter = {}
for word in sent:
    word_counter[word] = sent.count(word)
word_counter
```

Now after that you can easily retrieve the word count by accessing the `word_counter` dictionary using the word key and get the count (i.e. the value):

```python
num_the = word_counter['the'] # Use square brackets to access the dictionary using the key.
print (word_counter['the'])  
print (word_counter['jump'])
```

Similar to `list`, you can also set the values of a dictionary using comprehension, the following [**dictionary comprehension**](https://www.python.org/dev/peps/pep-0274/) achieves the same result as the for-loop we have above:

```python
sent = 'the quick brown fox jumps over the lazy dog'.split()
word_counter = {word:sent.count(word) for word in sent}
```

Note that the use of the colon when initializing a dictionary with `key:value` (e.g. `'the': 2` ). You can also initialize a dictionary manually (aka statically) like how we would initialize a list:

```python
list1 = [1, 2, 3, 4, 5]
dict1 = {'the': 2, 'quick':1 , 'brown': 1}
```

And other than the basic data container, you can use specialized data containers that can make your code looks cleaner and also use some of the nifty "batteries included" features. Instead of counting the words like we did using a dictionary comprehension, there is a specialized data container call [`collections.Counter`](https://docs.python.org/2/library/collections.html#collections.Counter). And to initlize the same `word_counter`, we can simply do this:


```python
from collections import Counter
sent = 'the quick brown fox jumps over the lazy dog'.split()
word_counter = Counter(sent)
word_counter
```

Tuple-ware
====

Unlike the other basic data container types, `tuple` is a special breed. In other contains, it is possible to append a new item to a list, add to a set and expand a dictionary, e.g.

```python
list1 = [6,1,2,7,3,4,2,6,3]
new_num = 100
list1.append(new_num) # Appends an element to a list.
set1 = set(list1)
set1.add(new_num) # Adds a new unique element to a set.

dict1 = {'the': 2, 'brown': 1, 'fox':1}
dict1['jumps'] = 1 # Extends a dictionary with a new key-value pair.
```

That ability to change the values in the data type is call **`mutuable`**. Unlike `list`, `set` and `dict`, `tuple` is an **`immutable`**

```python
list1 = [6,1,2,7,3,4,2,6,3]
tup1 = tuple(list1)
print (type(tup1))
tup1.add(100) # This will return an error.
tup1.append(100) # This will also return an error.
```

When trying to add/append to a tuple, you will see this error:

```python
>>> tup1.add(100)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'add'

>>> tup1.append(100)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'add'
```

The only two functions that a `tuple` type has is (i) to find the first instance of a particular item, e.g.:

```python
list1 = [6,1,2,7,3,4,2,6,3]
tup1 = tuple(list1)
tup1.index(3)
```

and the other function (ii) to count the number of instances of a particular item, e.g.:

```python
list1 = [6,1,2,7,3,4,2,6,3]
tup1 = tuple(list1)
tup1.count(3)
```

**So why do we need tuples when we can easily use a list?** See http://stackoverflow.com/a/1708538/610569. TL;DR cos iterating through a tuple is faster than a list.

----

Congratulations !!!
====

You have learnt more about built-ins and the various basic container types in python! 
