---
layout: category
title: RTOS Tutorials
permalink: /embedded/rtos/
tag: rtos
---
<div class="tutorial-layout">
  <aside class="tutorial-sidebar">
    <h2>Categories</h2>
    <ul>
      {% assign categories = site.data.categories.embedded %}
      {% for cat in categories %}
        <li><a href="#{{ cat.anchor }}">{{ cat.title }}</a></li>
      {% endfor %}
    </ul>
  </aside>

  <main class="tutorial-content">
    {% for cat in categories %}
      <section id="{{ cat.anchor }}">
        <h2>{{ cat.title }}</h2>
        <ul>
          {% assign posts = site.embedded | where_exp: "p", "p.tags contains cat.anchor" %}
          {% for post in posts %}
            <li>
              <a href="{{ post.url }}">{{ post.title }}</a>
              <p>{{ post.excerpt }}</p>
            </li>
          {% endfor %}
        </ul>
      </section>
    {% endfor %}
  </main>
</div>
