---
title: Categories
---
<div class="category-list">
  {% for category in site.categories %}
    {% assign sorted_posts = category[1] | sort: 'date' | reverse %}
    <section class="category-block" id="{{ category[0] | slugify }}" data-count="{{ category[1].size }}">
      <h3>{{ category[0] }}</h3>
      <ul>
        {% for post in sorted_posts %}
          <li>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            <span>{{ post.date | date: "%Y-%m-%d" }}</span>
          </li>
        {% endfor %}
      </ul>
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
