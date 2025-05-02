---
layout: default
title: cozumler
---

## Modül Çözümleri
<ul>
  {% assign modul_posts = site.posts | where_exp: "post", "post.categories contains 'modul'" %}
  {% for post in modul_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## Makine Çözümleri
<ul>
  {% assign makine_posts = site.posts | where_exp: "post", "post.categories contains 'makine'" %}
  {% for post in makine_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
