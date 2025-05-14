---
layout: default
title: Embedded Tutorials
permalink: /embedded/
---

{% assign categories = site.data.categories.embedded %}

<button id="toggleSidebar" class="sidebar-toggle">☰ Show Categories</button>

<div class="tutorial-layout">
  <aside class="tutorial-sidebar" id="sidebar">
    <h2>Categories</h2>
    <ul>
      {% for cat in categories %}
        <li>
          <a href="{{ '/embedded/' | append: cat.anchor | append: '/' | relative_url }}">
            {{ cat.title }}
          </a>
        </li>
      {% endfor %}
    </ul>
  </aside>

  <main class="tutorial-content">
    {% for cat in categories %}
      <section class="category-preview">
        <h2>{{ cat.title }}</h2>

        {% assign cat_posts = site.embedded | where_exp: "p", "p.tags contains cat.anchor" | sort: "date" | reverse %}
        {% assign latest = cat_posts[0] %}

        {% if latest %}
          <div class="category-card">
            <h3><a href="{{ latest.url | relative_url }}">{{ latest.title }}</a></h3>
            <p>{{ latest.excerpt }}</p>
            <a class="see-all" href="{{ '/embedded/' | append: cat.anchor | append: '/' | relative_url }}">
              See all {{ cat.title }} posts →
            </a>
          </div>
        {% else %}
          <p>No posts yet in this category.</p>
        {% endif %}
      </section>
    {% endfor %}
  </main>
</div>
