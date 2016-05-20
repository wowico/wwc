---
layout: page
title: Friends
---

Here are the biographies of friends who have successfully submitted at least one pull request.

{% assign pages_list = site.friends %}
{% for node in pages_list %}
{% if node.title != null %}
{% if node.title != "Friend (template)" %}
  {% if node.layout == "page" %}
  <a href="{{ site.baseurl }}{{ node.url }} ">{{ node.title }} </a>   
  {% endif %}
{% endif %}
{% endif %}
{% endfor %}