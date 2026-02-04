---
title: PostList
---
{% for category in site.categories %}
  <h3>{{ category[0] }}</h3>
  <div class="post-cards">
    {% for post in category[1] %}
      <a class="post-card" href="{{ post.url | relative_url }}" aria-label="{{ post.title }}">
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
        <div class="post-card-meta">{{ post.date | date: "%Y-%m-%d" }}</div>
      </a>
    {% endfor %}
  </div>
{% endfor %}
