---
layout: default
title: bloglar
---

# Bloglar

<div class="blog-listesi">
  {% for post in site.posts %}
    {% if post.categories contains "blog" %}
      <div class="blog-item">
        <div class="blog-description">
          <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
          <p>{{ post.desc }}</p>
        </div>
        <div class="blog-logo">
          <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} logo">
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>
