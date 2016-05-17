# Working With Corpora

This repository contains teaching materials for Saarland Uni's [*Working With Corpora*](http://fedora.clarin-d.uni-saarland.de/unserwiki/doku.php?id=training:working_with_corpora/) program. It's been adapted from the repository for teaching materials and additional resources used by [*Research Platforms Services*](http://melbourne.resbaz.edu.au/) at the University of Melbourne to teach *Python*, *IPython*, *Jupyter* and the *Natural Language Toolkit* (*NLTK*).

Essentially, the idea of both programs is to run free training in reproducible research methods and tools via [a cloud platform](https://dit4c.github.io/), so that nobody has to worry about installation/operating system/specs problems. All code is written and executed within [Jupyter Notebooks](http://jupyter.org/), allowing easy access to earlier input and output, as well as the rich display of text/images.

Learn more on [WwC Python sessions](http://fedora.clarin-d.uni-saarland.de/unserwiki/doku.php?id=training:python) at this URL. Want to join? Register by filling in this [form](https://docs.google.com/forms/d/1VThhhXYbrcKKe8p33tijzAIpbKHBqOcVsUyEcXDAu4Y/viewform). Subscribe to the [mailing list](https://groups.google.com/forum/#!forum/workingwithcorpora) and check the [calendar](https://calendar.google.com/calendar/embed?src=toccngu71401plkr8q4ccql75s@group.calendar.google.com&ctz=Europe/Berlin) to keep up-to-date with WwC activities.

All the materials used in the workshops are in this repository. In fact, cloning this repository will be our first activity together as a group. To do that, just open your terminal and type/paste:

```shell
git clone git@github.com:wowico/wwc.git
```

Our lessons are stored as *markdown* files. The following line of code will let us open *markdown* files in the *Jupyter Notebook*.

```shell
pip install notedown
printf "c.NotebookApp.contents_manager_class = 'notedown.NotedownContentsManager'\n" >> ~/.jupyter/jupyter_notebook_config.py
```
