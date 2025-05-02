---
layout: default
title: makine-cozumler
---

# Makine Çözümleri

<div class="makine-listesi">
  {% for post in site.posts %}
    {% if post.categories contains "makine" %}
      <div class="machine-item">
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <div class="machine-desc-with-logo">
          <p>{{ post.desc }}</p>
          <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} logo">
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>

