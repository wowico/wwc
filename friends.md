---
layout: page
title: Friends
---

This should link to all of our friends.

{% assign pages_list = site.friends %}
{% for node in pages_list %}
{% if node.title != null %}
{% if node.title != "Friend (template)" %}
  {% if node.layout == "page" %}
  <a href="{{ node.url }} ">{{ node.title }} </a>   
  {% endif %}
{% endif %}
{% endif %}
{% endfor %}