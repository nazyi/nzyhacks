---
layout: default
title: Write-ups
lang: en
permalink: /en/cozumler
translation_url: /cozumler
---

# Write-ups

<div class="page-section">
  <h2>Machine Write-ups</h2>
  {% assign makineler = site.posts | where: "lang", "en" | where: "categories", "makine" | sort: "order" %}
  {% include solution-list.html posts=makineler %}
</div>

<div class="page-section">
  <h2>Module Write-ups</h2>
  {% assign moduller = site.posts | where: "lang", "en" | where: "categories", "modul" | sort: "order" %}
  {% include solution-list.html posts=moduller %}
</div>

<div class="page-section">
  <h2>Documentation</h2>
  {% assign dokumanlar = site.posts | where: "lang", "en" | where: "categories", "dokumantasyon" | sort: "order" %}
  {% if dokumanlar.size == 0 %}
  <p>Posts about JumpCloud and Trend Micro are coming soon. 🌸</p>
  {% else %}
  {% include solution-list.html posts=dokumanlar %}
  {% endif %}
</div>
