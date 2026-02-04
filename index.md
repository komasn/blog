<div class="post-cards">
  {% for post in site.posts limit:5 %}
    <div class="post-card" aria-label="{{ post.title }}">
      <a class="post-card-link" href="{{ post.url | relative_url }}">
        <div class="post-card-thumb">
          {% assign content = post.content | strip_newlines %}
          {% assign first_image = "" %}
          {% if content contains '<img' and content contains 'src="' %}
            {% assign img_parts = content | split: '<img' %}
            {% assign img_tag = img_parts[1] %}
            {% if img_tag contains 'src="' %}
              {% assign parts = img_tag | split: 'src="' %}
              {% assign first_image = parts[1] | split: '"' | first %}
            {% endif %}
          {% elsif content contains '![' %}
            {% assign parts = content | split: '![' %}
            {% assign first_image = parts[1] | split: '(' | last | split: ')' | first %}
          {% endif %}

          {% if post.image %}
            {% assign post_image_first = post.image | slice: 0, 1 %}
            {% if post.image contains '://' or post_image_first == '/' %}
              <img src="{{ post.image }}" alt="{{ post.title }}">
            {% else %}
              <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
            {% endif %}
          {% elsif first_image != "" %}
            {% if first_image contains '{{' %}
              {% assign parts2 = first_image | split: "'" %}
              {% assign imgpath = parts2[1] %}
              <img src="{{ imgpath | relative_url }}" alt="{{ post.title }}">
            {% else %}
              {% assign first_image_first = first_image | slice: 0, 1 %}
              {% if first_image contains '://' or first_image_first == '/' %}
                <img src="{{ first_image }}" alt="{{ post.title }}">
              {% else %}
                <img src="{{ first_image | relative_url }}" alt="{{ post.title }}">
              {% endif %}
            {% endif %}
          {% else %}
            <img src="{{ '/assets/images/logo.jpeg' | relative_url }}" alt="{{ post.title }}">
          {% endif %}
        </div>
        <div class="post-card-title">
          {{ post.title }}
        </div>
      </a>
      {% if post.categories %}
        <div class="post-card-categories">
          {% for category in post.categories %}
            <a class="post-category" href="{{ '/categories.html' | relative_url }}#{{ category | slugify }}">{{ category }}</a>
          {% endfor %}
        </div>
      {% endif %}
      <div class="post-card-meta">{{ post.date | date: "%Y-%m-%d" }}</div>
    </div>
  {% endfor %}
</div>

<p>
  <a href="{{ '/list.html' | relative_url }}">and more</a>
</p>
