---
layout: default
title: makine-cozumler
---

# Makine Çözümleri

{% assign platforms = "HTB,TryHackMe,CyberExam" | split: "," %}

{% for platform in platforms %}
  <h2 style="color:#FF69B4;">{{ platform }}</h2>
  <div class="makine-listesi">
    {% for post in site.posts %}
      {% if post.categories contains "makine" and post.tags contains platform %}
        <div class="machine-item">
          <div class="machine-description">
            <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
            <p>{{ post.desc }}</p>
          </div>
          <div class="machine-logo">
            <img src="{{ post.logo | relative_url }}" alt="{{ post.title }} logo">
          </div>
        </div>
      {% endif %}
    {% endfor %}
  </div>
{% endfor %}
