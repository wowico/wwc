---
layout: page
title: Adding your bio
author: Daniel
---

By the end of the first lesson, we want you to have submitted a *pull request*, which will add some information about you to this site. You'll already have forked our repository, so what you'll need to do is:

1. Checkout the `gh-pages` branch
2. Create a markdown file containing a short bio
3. Add the changes to your fork
4. Request that the changes be merged into the main repository.

So, from the *Shell Terminal*:

```shell
# go to fork
cd wwc
# select the website, not the lessons
git checkout gh-pages
```

Now, you can duplicate the template file:

```shell
# take a look at the template
cat _friends/friend.md
# copy it 
cp _friends/friend.md _friends/<yourname>.md
```

Once you've created it, go back to the *Jupyter Notebook*, open it up, and edit it to your liking.

When you're done, you need to upload your local changes to your remote fork:

```shell
# look at changed files
git status
# stage your file
git add _friends/<name>.md
# commit the changes
git commit -a "add my bio to the website"
# send to the remote
git push origin gh-pages
```

Problem? You'll probably need to register yourself:

```shell
git config --global user.name "Firstname Lastname"
git config --global user.email username@gmail.com
```

Try again:

```shell
git push origin gh-pages
```

Now, you can go to your fork on GitHub and make a pull request!