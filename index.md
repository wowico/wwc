---
title: Introduction
tags: [getting-started]
type: first_page
homepage: true
layout: default
---

Welcome!
---------

*Working with Corpora (wowico) provides free, open-source lessons relating to corpus linguistics at Saarland Uni.*

*The main point of this site, right now, is to show students how to use GitHub, GitHub Pages and markdown. It also functions as a blog, which everyone is welcome to contribute to.*

Recent blog posts
-------------------

{% for page in site.posts %}
{% if page.title != "Template" %}
  <h3><a href="{{ site.baseurl }}{{ page.url }}">{{ page.title }}</a></h3>
  <p>{{ page.content }}</p>
  {% endif %}
{% endfor %}
