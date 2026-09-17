---
layout: default
title: Etiketler
translation_url: /en/tags
---

# Etiketler

{% assign lang_posts = site.posts | where: "lang", "tr" %}
{% assign tag_string = "" %}
{% for post in lang_posts %}
  {% if post.tags %}
    {% assign joined = post.tags | join: "|||" %}
    {% assign tag_string = tag_string | append: joined | append: "|||" %}
  {% endif %}
{% endfor %}
{% assign all_tags = tag_string | split: "|||" | uniq | sort %}

{% for tag_name in all_tags %}
  {% assign tag_posts = lang_posts | where_exp: "post", "post.tags contains tag_name" %}
  <div class="page-section" id="{{ tag_name | slugify }}">
    <h2>{{ tag_name }}</h2>
    {% include solution-list.html posts=tag_posts %}
  </div>
{% endfor %}
