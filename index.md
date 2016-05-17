---
title: Introduction
tags: [getting-started]
type: first_page
homepage: true
layout: default
---

This is now our homepage.

{% for page in site.posts %}
  <h3><a href="{{ page.url }}">{{ page.title }}</a></h3>
  <p>{{ page.content }}</p>
{% endfor %}
