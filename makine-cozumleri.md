
---
layout: default
title: Makine Çözümleri
permalink: /makine-cozumleri/
---

<h1>Makine Çözümleri</h1>

<ul>
  {% for post in site.posts %}
    {% if post.categories contains 'makine' %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
