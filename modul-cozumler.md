---
layout: default
title: modul-cozumler
---

# Modül Çözümleri

<div class="modul-listesi">
  {% for post in site.posts %}
    {% if post.categories contains "modul" %}
      <div class="modul-item">
        <div class="machine-modul">
          <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
          <p>{{ post.desc }}</p>
        </div>
        <div class="modul-logo">
          <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} logo">
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>
