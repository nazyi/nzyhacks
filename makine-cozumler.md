---
layout: default
title: makine-cozumler
---

# Makine Çözümleri

{% assign makineler = site.posts | where: "categories", "makine" | sort: "order" %}

<div class="makine-listesi">
  {% for post in makineler %}
      <div class="machine-item">
        <div class="machine-description">
          <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
          <p>{{ post.desc }}</p>
        </div>
        <div class="machine-logo">
          <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} logo">
        </div>
      </div>
  {% endfor %}
</div>
