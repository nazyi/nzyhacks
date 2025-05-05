---
layout: default
title: modul-cozumler
---

# Modül Çözümleri

{% assign moduller = site.posts | where: "categories", "modul" | sort: "order" %}

<div class="modul-listesi">
  {% for post in moduller %}
    <div class="modul-item">
      <div class="modul-desciption">
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p>{{ post.desc }}</p>
      </div>
      <div class="modul-logo">
        <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} logo">
      </div>
    </div>
  {% endfor %}
</div>
