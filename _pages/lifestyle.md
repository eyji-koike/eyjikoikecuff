---
layout: default
title: Lifestyle
permalink: /lifestyle/
---
{% for post in site.lifestyle %}
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p>{{ post.excerpt }}</p>
{% endfor %}