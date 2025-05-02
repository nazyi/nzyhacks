---
layout: default
title: makine-cozumler
---

# Makine Çözümleri

<div class="makine-listesi">
  {% for post in site.posts %}
    {% if post.categories contains "makine" %}
      <div class="machine-item">
        <!-- Solda başlık ve açıklama -->
        <div class="machine-description">
          <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
          <p>{{ post.desc }}</p>
        </div>

        <!-- Sağda logo -->
        <div class="machine-logo">
          <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} Logo">
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>
