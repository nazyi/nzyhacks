---
layout: default
title: Documentation
lang: en
permalink: /en/dokumantasyon
translation_url: /dokumantasyon
---

# Documentation

I collect my setup, configuration, and usage notes on enterprise tools here.

{% assign dokumanlar = site.posts | where: "lang", "en" | where: "categories", "dokumantasyon" | sort: "order" %}

{% if dokumanlar.size == 0 %}
<p>Posts about JumpCloud and Trend Micro are coming soon. 🌸</p>
{% else %}
{% assign gruplar = dokumanlar | group_by: "tool" %}
<div class="doc-tabs">
  <div class="doc-tab-buttons">
    {% for grup in gruplar %}
      <button type="button" class="doc-tab-btn{% if forloop.first %} active{% endif %}" data-tab="doc-tab-{{ grup.name | slugify }}">{{ grup.name }}</button>
    {% endfor %}
  </div>
  <div class="doc-tab-content">
    {% for grup in gruplar %}
      <div class="doc-tab-panel{% if forloop.first %} active{% endif %}" id="doc-tab-{{ grup.name | slugify }}">
        {% include solution-list.html posts=grup.items %}
      </div>
    {% endfor %}
  </div>
</div>
{% endif %}
