---
layout: default
title: RTOS Tutorials
permalink: /embedded/rtos/
tag: rtos
collection: embedded
---

<div class="tutorial-layout">
  <aside class="tutorial-sidebar">
    <h2>Categories</h2>
    <ul>
      {% assign categories = site.data.categories.embedded %}
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
  <h2>{{ page.title }}</h2>
 <div class="filter-controls">
  <input type="text" id="searchInput" placeholder="Search by title..." />
  <select id="tagFilter">
    <option value="">All Tags</option>
    {% assign all_tags = site.embedded | map: "tags" | join: "," | split: "," | uniq | sort %}
    {% for tag in all_tags %}
      <option value="{{ tag | strip }}">{{ tag | capitalize }}</option>
    {% endfor %}
  </select>
  <button id="clearFilters">Clear</button>
</div>
<div class="post-grid" id="postGrid">
  {% assign posts = site.embedded | where_exp: "p", "p.tags contains page.tag" | sort: 'date' | reverse %}
  {% for post in posts %}
    <div class="post-card"
         data-title="{{ post.title | downcase }}"
         data-tags="{{ post.tags | join: ' ' | downcase }}">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>

      <p class="post-meta">
        {{ post.date | date: "%B %d, %Y" }}
      </p>

      <div class="tag-list">
        {% for tag in post.tags %}
          <span class="tag-pill">{{ tag }}</span>
        {% endfor %}
      </div>

      <p>{{ post.excerpt }}</p>
      <a class="read-more" href="{{ post.url | relative_url }}">Read more →</a>
    </div>
  {% endfor %}
</div>
<script>
  const searchInput = document.getElementById('searchInput');
  const tagFilter = document.getElementById('tagFilter');
  const clearBtn = document.getElementById('clearFilters');
  const cards = document.querySelectorAll('.post-card');

  function filterPosts() {
    const query = searchInput.value.toLowerCase();
    const selectedTag = tagFilter.value.toLowerCase();

    cards.forEach(card => {
      const title = card.dataset.title;
      const tags = card.dataset.tags;

      const matchTitle = title.includes(query);
      const matchTag = !selectedTag || tags.includes(selectedTag);

      card.style.display = (matchTitle && matchTag) ? 'block' : 'none';
    });
  }

  searchInput.addEventListener('input', filterPosts);
  tagFilter.addEventListener('change', filterPosts);
  clearBtn.addEventListener('click', () => {
    searchInput.value = '';
    tagFilter.value = '';
    filterPosts();
  });
</script>

</main>

</div>

