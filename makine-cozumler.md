---
layout: default
title: makine-cozumler
---

# Makine Çözümleri

<ul>
  {% for post in site.posts %}
    {% if post.categories contains "makine" %}
      <li class="machine-item">
        <!-- Solda başlık ve açıklama -->
        <div class="machine-description">
          <h3>{{ post.title }}</h3>
          <p>{{ post.desc }}</p>
        </div>
        
        <!-- Sağda logo -->
        <div class="machine-logo">
          <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} Logo" />
        </div>
      </li>
    {% endif %}
  {% endfor %}
</ul>
