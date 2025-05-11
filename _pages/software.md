---
layout: default
title: Software Tutorials
permalink: /software/
---
{% for post in site.software %}
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p>{{ post.excerpt }}</p>
{% endfor %}