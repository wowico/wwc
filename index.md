---
title: Introduction
tags: [getting-started]
type: first_page
homepage: true
layout: default
---

Working with Corpora (wowico) is an organisation that gives open-source lessons relating to corpus linguistics at Saarland Uni.

The main point of this site, right now, is to show students how to use GitHub, GitHub Pages and markdown.

```shell
# select the website, not the lessons
git checkout gh-pages
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

{% for page in site.posts %}
{% if page.title != "Template" %}
  <h3><a href="{{ site.baseurl }}{{ page.url }}">{{ page.title }}</a></h3>
  <p>{{ page.content }}</p>
  {% endif %}
{% endfor %}
