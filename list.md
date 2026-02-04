---
title: PostList
---
<div class="category-list">
  {% for category in site.categories %}
    <section class="category-block" data-count="{{ category[1].size }}">
      {% assign sorted_posts = category[1] | sort: 'date' | reverse %}
      <h3>{{ category[0] }}</h3>
      <ul>
        {% for post in sorted_posts limit: 5 %}
          <li>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            <span>{{ post.date | date: "%Y-%m-%d" }}</span>
          </li>
        {% endfor %}
      </ul>
      {% if category[1].size > 5 %}
        <p>
          <a href="{{ '/categories.html' | relative_url }}#{{ category[0] | slugify }}">and more</a>
        </p>
      {% endif %}
    </section>
  {% endfor %}
</div>

<script>
  (function () {
    var container = document.querySelector('.category-list');
    if (!container) return;
    var blocks = Array.prototype.slice.call(
      container.querySelectorAll('.category-block')
    );
    blocks
      .sort(function (a, b) {
        return Number(b.dataset.count) - Number(a.dataset.count);
      })
      .forEach(function (block) {
        container.appendChild(block);
      });
  })();
</script>
