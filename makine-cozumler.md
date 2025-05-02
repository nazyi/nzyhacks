---
layout: default
title: makine-cozumler
---

# Makine Çözümleri

<div class="machine-list">
  {% for post in site.posts %}
    {% if post.categories contains "makine" %}
      <div class="machine-item">
        <div class="machine-info">
          <h3>{{ post.title }}</h3>
          <p>{{ post.desc }}</p>
        </div>
        <div class="machine-logo">
          <img src="{{ post.logo }}" alt="{{ post.title }} Logo" />
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>
