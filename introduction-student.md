# Introduction

Welcome to *Jupyter*. Through this interface, you'll be learning a lot of things:

* A Programming language: **Python**
* A Python library: **NLTK**
* Overlapping research areas: **Corpus linguistics**, **Natural language processing**, **Distant reading**
* Additional skills: **Regular Expressions**, some **Shell commands**, and **tips on managing your data**

Quick links:

* Our repository (including wiki): [https://github.com/wowico/wwc](https://github.com/wowico/wwc).
* Our blog: [http://wowico.github.io/wwc/](http://wowico.github.io/wwc/)

Remember, everything we cover here will remain available to you after we're through is over, including a completed version of these notebooks. It's all accessible via [GitHub](https://github.com/wowico/wwc).

**Any questions before we begin?**

Alright, we're off!

## Text as data

Programming languages like Python are great for processing data. In order to apply it to *text*, we need to think about our text as data. This means being aware of how text is structured, what extra information might be encoded in it, and how to manage to give the best results.

The Natural Language Toolkit contains bits and pieces for working with text as data. It's a large library, and by default, it doesn't come with all its data files (corpora, tokeniser models, etc.). So, our first step here is to download this stuff.

```python
import nltk # Use for importing the nltk library

user_nltk_dir = "/home/researcher/nltk_data" # Specify our data directory
if user_nltk_dir not in nltk.data.path: # Make sure nltk can access this dir.
    nltk.data.path.insert(0, user_nltk_dir)
nltk.download("book", download_dir=user_nltk_dir, quiet=True) # Download book materials to data dir
```

With that out of the way, we're ready to code!

```python

```