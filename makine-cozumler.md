---
layout: default
title: "Makine Çözümleri"
---

# Makine Çözümleri

<ul>
  {% for post in site.posts %}
    {% if post.categories contains "makine" %}
      <li>
        <a href="{{ post.url }}">
          <img src="{{ post.logo }}" alt="{{ post.title }} Logo" width="50" />
          <strong>{{ post.title }}</strong>: {{ post.desc }}
        </a>
      </li>
    {% endif %}
  {% endfor %}
</ul>
