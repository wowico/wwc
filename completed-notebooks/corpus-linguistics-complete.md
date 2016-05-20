# Session 2: Common NLTK tasks

In this session we provide an quick introduction to the field of *corpus linguistics*. We then engage with common uses of NLTK within these areas, such as sentence segmentation, tokenisation and stemming. Often, NLTK has inbuilt methods for performing these tasks. As a learning exercise, however, we will sometimes build basic tools from scratch.

## Corpus linguistics

Though corpus linguistics has been around since the 1950s, it is only in the last 20 years that its methods have been made available to individual researchers. GUIs including [Wordsmith Tools](http://www.lexically.net/wordsmith/) and [AntConc](http://www.laurenceanthony.net/software.html).

Alongside the development of GUIs, there has also been a shift from *general, balanced corpora* (corpora seeking to represent a language generally) toward *specialised corpora* (corpora containing texts of one specific type, from one speaker, etc.). More and more commonly, texts are taken from the Web.

> We'll discuss building corpora from online texts in a bit more detail later in the course.

After a long period of resistance, corpus linguistics has gained acceptence within a number of research areas. A few popular applications are within:

* **Lexicography** (creating usage-based definitions of words and locating real examples)
* **Language pedagogy** (advanced language learners can use a concordancing GUI or collocation tests to understand how certain words are used in the target language)
* **Discourse analysis** (researching how meaning is made beyond the level of the clause/sentence)

Notably, corpus linguistic methods have been embraced within the emerging paradigm of Digital Humanities, where it's sometimes called *distant reading*.

### Corpora and discourse

As hardware, software and data become more and more available, people have started using corpus linguistic methods for discourse-analytic work. Paul Baker refers the combination of corpus linguistics and (critical) discourse analysis as a [*useful methodological synergy*](#ref:baker). Corpora bring objectivity and empiricism to a qualitative, interpretative tradition, while discourse- analytic methods provide corpus linguistics with a means of contextualising abstracted results.

Within this area, researchers rely on corpora to varying extents. In *corpus-driven* discourse analysis, researchers interpret the corpus based on the findings of the corpus interrogation. In *corpus-assisted* discourse analysis, researchers may use corpora to provide evidence about the way a given person/idea/discourse is commonly represented by certain people/in certain publications etc.

Our work here falls under the *corpus-driven* heading, as we are exploring the dataset without any major hypotheses in mind.

> Some linguists remain skeptical of corpus linguistics generally. In
a well-known critique, Henry Widdowson ([2000, p. 6-7](#ref:widdowson)) said:
>
> Corpus linguistics \[...\] (there) is no doubt that this is an immensely important development in descriptive linguistics. That is not the issue here. The quantitative analysis of text by computer reveals facts about actual language behaviour which are not, or at least not immediately, accessible to intuition. There are frequencies of occurrence of words, and regular patterns of collocational co-occurrence, which users are unaware of, though they must be part of their competence in a procedural sense since they would not otherwise be attested. They are third person observed data ('When do they use the word X?') which are different from the first person data of introspection ('When do I use the word X?'), and the second person data of elicitation ('When do you use the word X?'). Corpus analysis reveals textual facts, fascinating profiles of produced language, and its concordances are always springing surprises. They do indeed reveal a reality about language usage which was hitherto not evident to its users.
>
> But this achievement of corpus analysis at the same time necessarily defines its limitations. For one thing, since what is revealed is contrary to intuition, then it cannot represent the reality of first person awareness. We get third person facts of what people do, but not the facts of what people know, nor what they think they do: they come from the perspective of the observer looking on, not the introspective of the insider. In ethnomethodogical terms, we do not get member categories of description. Furthermore, it can only be one aspect of what they do that is captured by such quantitative analysis. For, obviously enough, the computer can only cope with the material products ofwhat people do when they use language. It can only analyse the textual traces of the processes whereby meaning is achieved: it cannot account for the complex interplay of linguistic and contextual factors whereby discourse is enacted. It cannot produce ethnographic descriptions of language use. In reference to Hymes's components of communicative competence (Hymes 1972), we can say that corpus analysis deals with the textually attested, but not with the encoded possible, nor the contextually appropriate.
>
> To point out these rather obvious limitations is not to undervalue corpus analysis but to define more clearly where its value lies. What it can do is reveal the properties of text, and that is impressive enough. But it is necessarily only a partial account of real language. For there are certain aspects of linguistic reality that it cannot reveal at all. In this respect, the linguistics of the attested is just as partial as the linguistics of the possible.

## Loading a corpus

First, we have to load a corpus. We'll use a text file containing posts to [an Australian online forum](http://www.ozpolitic.com/forum/YaBB.pl?board=global) for discussing politics. It's full of very interesting natural language data!

This file is available online, at the Research Platforms [GitHub](https://github.com/resbaz/nltk). We can ask Python to get it for us.

> Later in the course, we'll discuss how to extract data from the Web and turn this data into a corpus.

```python
import requests # a library for working with urls 
url = 'http://git.io/v47HI'
# url = "https://raw.githubusercontent.com/resbaz/nltk/master/corpora/oz_politics/ozpol.txt" # define the url
response = requests.get(url) # `verify=False` if need be
raw_text = response.text
raw_text = raw_text.lower() # make it lowercase, to keep things simple
len(raw_text) # how many characters does it contain?
raw_text[:2000] # first 2000 characters
```

Let's save the corpus to our cloud as a text file.

```python
with open('forum.txt', 'w', encoding = 'utf-8') as fo:
    fo.write(raw_text)
```

```python
with open('forum.txt', 'r', encoding = 'utf-8') as fo:
    loaded_raw_text = f.read().lower()
print(loaded_raw_text[:2000])
```

## Sentence segmentation

We can now start to turn our corpus into a structured resource. At present, we have `raw_text`, a very, very long string of text.

We should break the string into segments. First, we'll split the corpus into sentences. This task is a pretty boring one, and it's tough for us to improve on existing resources.

```python
import nltk.data
sent_tokenizer=nltk.data.load('tokenizers/punkt/english.pickle')
sents = sent_tokenizer.tokenize(raw_text)
sents[101:111]
```

Alright, we have sentences. Now what?

## Tokenisation

Tokenisation is simply the process of breaking texts down into words. We already did a little bit of this in Session 1. We won't build our own tokenizer, because it's not much fun. NLTK has one we can rely on.

Keep in mind that definitions of tokens are not standardised, especially for languages other than English. Serious problems arise when comparing two corpora that have been tokenised differently.

```python
tokenized_sents = [nltk.word_tokenize(i) for i in sents]
tokenized_sents[:10]
```

What we have is a list of lists: sentences and their tokens. We might also want to flatten the list:

```python
flat = sum(tokenized_sents, [])
```

... the sentence segmentation is still important, however, as it helped with proper handling of sentence final punctuation, for example.

Let's jump quickly into analysing the corpus. Like in the last lesson, we might want to count tokens. That can be very simple:

```python
def howmany(word):
    return sum([s.count(word) for s in tokenized_sents])
```

```python
howmany('the')
```

Cool. Two problems, though. First, this takes one word of interest at a time. Second, we can only search for literal words.

## Loops

A common programming method for reperforming some function is the *loop*. Most prototypical is the *for loop*:

```python
list(range(10))
```

```python
for i in range(10):
    print(i)
```

So, how would we put this to work with our `howmany()` function?

```python
wordlist = ['terror', 'refugee', 'refugees', 'islam']
for word in wordlist:
    print(word, howmany(word))
```

Powerful, eh? The next problem, however, is that we're stuck writing out `refugee` and `refugees`.

## Regular expressions

Regular expressions are a language for searching strings of characters. For us right now, they're a language inside a language. Alphanumeric characters and some punctuation work just like normal searches, but some special characters have different meanings. You've probably already seen some of these in the wild, like the asterisk as wildcard.

At their simplest, we can check if a string matches a regex:

```python
print(re.match('^T', 'this'))
```

Or to print strings matching our criteria:

```python
import re
set(re.findall(r'[a-z]+ing\b', raw_text)[:20])
```

Let's use regular expressions to search our non-segmented text:

```python
re.findall('muslims?', raw_text)
re.findall('.*storm.*', raw_text)
re.findall('[^\s]+ muslims? [^\s]+', raw_text)
from collections import Counter
Counter(re.findall('([^\s]+) muslims? [^\s]+', raw_text)).most_common()
```

We can use this kind of approach to start matching nouns and their plurals:

```python
re.findall(r'([a-z]+(es|s))', raw_text)
```

Or we could use it to stem our text:

```python
regex = re.compile(r'([a-z]+)(ing|s|ed|er)([^a-z])')
re.sub(regex, r'\1\3', raw_text)[:2000]
```

Can you update `howmany()` to handle:

1. Regular expressions
2. A tokenised corpus

```python
def howmany(regex):
    import re
    return len([i for i in flat if re.match(regex, i)])

def howmany(regex):
    c = 0
    for i in flat:
        if re.match(regex, i):
            c += 1
    return c

howmany(r'musl[a-sz]')
```

There are limits to this kind of approach, though. What are they?

## Stemming

Stemming is the task of finding the stem of a word. So, *cats --> cat*, or *taking --> take*. It is an important task when counting words, as often the counting each inflection seperately is not particuarly helpful: forms of the verb 'to be' might seem under-represented if we could *is, are, were, was, am, be, being, been* separately.

NLTK has pre-programmed stemmers, but we can build our own using some of the skills we've already learned.

A stemmer is the kind of thing that would make a good function, so let's do that.

```python
def stem(word):
    for suffix in ['ing', 'ly', 'ed', 'ious', 'ies', 'ive', 'es', 's', 'ment']: # list of suffixes
        if word.endswith(suffix):
            return word[:-len(suffix)] # delete the suffix
    return word
```

Give it a word to stem!

```python
stem('friends')
```

Let's run it over some text and see how it performs.

```python
for sent in tokenized_sents[:5]:
    for token in sent:
        print(stem(token))
```

Looking at the output, we can see that the stemmer works: *wingers* becomes *winger*, and *tearing* becomes *tear*. But, sometimes it does things we don't want: *Nothing* becomes *noth*, and *mate* becomes *mat*.

We can see that this approach has obvious limitations. So, let's rely on a purpose-built stemmer. These rely in part on dictionaries. Note the subtle differences between the two possible stemmers.

Now we can try our NLTK's stemmers!

```python
# instantiate stemmers
lancaster = nltk.LancasterStemmer()
porter = nltk.PorterStemmer()

# stem each word in tokens
stems = [lancaster.stem(t) for t in flat]  # replace lancaster with porter here
print(stems[:100])
```

Notice that both stemmers handle some things rather poorly. The main reason for this is that they are not aware of the *word class* of any particular word: *nothing* is a noun, and nouns ending in *ing* should not have *ing* removed by the stemmer (swing, bling, ring...). Later in the course, we'll start annotating corpora with grammatical information. This improves the accuracy of stemmers a lot.

> Note: stemming is not *always* the best thing to do: though *thing* is the stem of *things*, things has a unique meaning, as in *things will improve*. If we are interested in vague language, we may not want to collapse things --> thing.

## Collocation

> *You shall know a word by the company it keeps.* - J.R. Firth, 1957

Collocation is a very common area of interest in corpus linguistics. Words pattern together in both expected and unexpected ways. In some contexts, *drug* and *medication* are synonymous, but it would be very rare to hear about *illicit* or *street medication*. Similarly, doctors are unlikely to prescribe the *correct* or *appropriate drug*.

This kind of information may be useful to lexicographers, discourse analysts, or advanced language learners.

In NLTK, collocation works from ordered lists of tokens. We made this earlier as `tokens`, didn't we?

```python
print(flat[:50])
```

If not, here:

```python
flat = sum(tokenized_sents, [])
```

Now, let's feed these to an NLTK function for measuring collocations:

```python
# get all the functions needed for collocation work
from nltk.collocations import *
# define statistical tests for bigrams
bigram_measures = nltk.collocations.BigramAssocMeasures()
# go and find bigrams
finder = BigramCollocationFinder.from_words(flat)
# measure which bigrams are important and print the top 30
print(sorted(finder.nbest(bigram_measures.raw_freq, 30)))
```

So, that tells us a little: we can see that terrorists, Muslims and the Middle
East are commonly collocating in the text. At present, we are only looking for
immediately adjacent words. So, let's expand out search to a window of *five
words either side*

```python
# ''window size'' specifies the distance at which 
# two tokens can still be considered collocates
finder = BigramCollocationFinder.from_words(flat, window_size=5)
print(sorted(finder.nbest(bigram_measures.raw_freq, 30)))
```

Now we have the appearance of very common words! Let's use NLTK's stopwords list
to remove entries containing these:

```python
def ignorer(w):
    ignored_words = nltk.corpus.stopwords.words('english')
    return w.lower() in ignored_words

finder.apply_word_filter(ignorer)
print(sorted(finder.nbest(bigram_measures.raw_freq, 30)))
```

There! Now we have some interesting collocates. Finally, let's remove
punctuation-only entries, or entries that are *n't*, as this is caused by
different tokenisers:

```python
def ignorer(w):
    ignored_words = nltk.corpus.stopwords.words('english')
    return w.lower() in ignored_words or not w.isalnum()

finder.apply_word_filter(ignorer)
print(sorted(finder.nbest(bigram_measures.raw_freq, 30)))
```

You can get a lot more info on collocation at the [NLTK homepage](http://www.nltk.org/howto/collocations.html).

Completed bigrams code:

```python
def ignorer(w):
    ignored_words = nltk.corpus.stopwords.words('english')
    return w.lower() in ignored_words or not w.isalnum()

# get all the functions needed for collocation work
from nltk.collocations import *
bigram_measures = nltk.collocations.BigramAssocMeasures()
finder = BigramCollocationFinder.from_words(flat)
finder.apply_word_filter(ignorer)
print(sorted(finder.nbest(bigram_measures.raw_freq, 30)))
```

## Clustering/n-grams

Clustering is the task of finding words that are commonly **immediately** adjacent (as opposed to collocates, which may just be nearby). This is also often called n-grams: bigrams are two tokens that appear together, trigrams are three, etc.

Clusters/n-grams have a spooky ability to tell us what a text is about.

There's also a method for n-gram production in NLTK. We can use this to understand how n-gramming works.

Below, we get lists of any ten adjacent tokens:

```python
from nltk.util import ngrams
# define a sentence
sentence = 'give a man a fish and you feed him for a day; teach a man to fish and you feed him for a lifetime'  
tokenised = nltk.word_tokenize(sentence)
# length of ngram
n = 10
tengrams = list(ngrams(tokenised, n))
print(tengrams)
```

So, there are plenty of tengrams in there! What we're interested in, however, is
duplicated n-grams:

```python
def ngrammer(text, gramsize = 3, threshold = 4):
    """get ngrams of gramsize size and threshold minimum occurrences"""
    if type(text) != list:
        text = nltk.word_tokenize(text)
    # skip punctuation? stopwords?
    # 
    ngms = ngrams(text, gramsize)
    cntr = Counter(ngms)
    return [(gram, freq) for gram, freq in cntr.most_common() if freq >= threshold]
```

Now that it's defined, let's run it, looking for trigrams

```python
ngrammer(flat, gramsize = 2).most_common(10)
```

Whoops, punctutation.

```python
# add me:
text = [token for token in text if token.isalnum() and token not in ignored_words]

```

Too many results? Let's set a higher threshold than the default.

```python
ngrammer(raw, gramsize = 3, threshold = 10)
```


## Concordancing with regular expressions

We've already done a bit of concordancing. In discourse-analytic research, concordancing is often used to perform thematic categorisation.

```python
text = nltk.Text(flat)  # formats our tokens for concordancing
text.concordance("muslims")
```

A problem with the NLTK concordancer is that it only works with individual tokens. What if we want to find words that end with **ment*, or words beginning with *poli**?

We already searched text with Regular Expressions. It's not much more work to build regex functionality into our own concordancer.

From running the code below, you can see that bracketting sections of our regex causes results to split into lists:
```

```python
re.findall(r'(ozz?|auss)(ie)(s)?', raw_text)
```

We can use this same principle to get co-text:

```python
re.findall(r'(.*)(aussies?)(.*)', raw_text)
```

Well, it's ugly, but it works. We can see five bracketted results, each containing three strings. The first and third strings are the left-context and right-context. The second of the three strings is the search term.

These three sections are, with a bit of tweaking, the same as the output given by a concordancer.

Let's go ahead and turn our regex seacher into a concordancer:

```python
def conc(query, text):
    """regex concordancer"""
    import re
    compiled = re.compile(r'(.*)(%s)(.*)' % query)
    lines = re.findall(compiled, text)
    for start, middle, end in lines:
        concline = [start[-30:], middle, end[:30]]
        print("\t".join(concline).expandtabs(35))
```

```python
concordancer('austral[a-z]+', raw_text)
```

Great! With six lines of code, we've officially created a function that improves on the one provided by NLTK! And think how easy it would be to add more functionality: an argument dictating the size of the window (currently 30 characters), or printing line numbers beside matches, would be pretty easy to add, as well.

> Adding too much functionality is known as *feature creep*. It's often best to keep your functions simple and more varied. An old adage in programming is to *make each program do one thing well*.

In the cells below, try concordancing a few things. Also try creating variables with concordance results, and then manipulate the lists. If you encounter problems with the way the concordancer runs, alter the function and redefine it. If you want, try implementing the window size variable!

> If you wanted to get really creative, you could try stemming concordance or n-gram results!

## Summary

That's the end of session three! Great work.

So, some of these tasks are a little dry---seeing results as lists of words and scores isn't always a lot of fun. But ultimately, they're pretty important things to know if you want to avoid the 'black box approach', where you simply dump words into a machine and analyse what the machine spits out.

Remember that almost every task in corpus linguistics/distance reading depends on how we segment our data into sentences, clauses, words, etc.

Building a stemmer from scratch taught us how to use regular expressions, and their power. But, we also saw that they weren't perfect for the task. In later lessons, we'll use more advanced methods to normalise our data.

# Bibliography

<a id="ref:baker"></a>
Baker, P., Gabrielatos, C., Khosravinik, M., Krzyzanowski, M., McEnery, T., &
Wodak, R. (2008). A useful methodological synergy? Combining critical discourse
analysis and corpus linguistics to examine discourses of refugees and asylum
seekers in the UK press. Discourse & Society, 19(3), 273-306.

<a id="firth"></a>
Firth, J. (1957).  *A Synopsis of Linguistic Theory 1930-1955*. In: Studies in
Linguistic Analysis, Philological Society, Oxford; reprinted in Palmer, F. (ed.)
1968 Selected Papers of J. R. Firth, Longman, Harlow.

<a id="ref:hymes"></a>
Hymes, D. (1972). On communicative competence. In J. Pride & J. Holmes (Eds.),
Sociolinguistics (pp. 269-293). Harmondsworth: Penguin Books. Retrieved from [ht
tp://humanidades.uprrp.edu/smjeg/reserva/Estudios%20Hispanicos/espa3246/Prof%20S
unny%20Cabrera/ESPA%203246%20-%20On%20Communicative%20Competence%20p%2053-73.pdf
](http://humanidades.uprrp.edu/smjeg/reserva/Estudios%20Hispanicos/espa3246/Prof
%20Sunny%20Cabrera/ESPA%203246%20-%20On%20Communicative%20Competence%20p%2053-73
.pdf)

<a id="ref:widdowson"></a>
Widdowson, H. G. (2000). On the limitations of linguistics applied. Applied
Linguistics, 21(1), 3. Available at [http://applij.oxfordjournals.org/content/21
/1/3.short](http://applij.oxfordjournals.org/content/21/1/3.short).
