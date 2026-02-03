<div class="post-cards">
  {% for post in site.posts %}
    <div class="post-card">
      <div class="post-card-thumb">
        {% if post.image %}
          <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
        {% else %}
          <img src="{{ '/assets/images/logo.jpeg' | relative_url }}" alt="{{ post.title }}">
        {% endif %}
      </div>
      <div class="post-card-title">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </div>
      <div class="post-card-meta">{{ post.date | date: "%Y-%m-%d" }}</div>
      <div class="post-card-excerpt">
        {{ post.excerpt | strip_html | truncate: 120 }}
      </div>
    </div>
  {% endfor %}
</div>
