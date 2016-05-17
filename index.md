---
title: Introduction
tags: [getting-started]
type: first_page
homepage: true
layout: default
---

Recent posts
-------------------

{% for page in site.posts %}
{% if page.title != "Template" %}
  <h3><a href="{{ site.baseurl }}{{ page.url }}">{{ page.title }}</a></h3>
  <p>{{ page.content }}</p>
  {% endif %}
{% endfor %}
