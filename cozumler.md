---
layout: default
title: Çözümler
translation_url: /en/cozumler
---

# Çözümler

<div class="page-section">
  <h2>Makine Çözümleri</h2>
  {% assign makineler = site.posts | where: "lang", "tr" | where: "categories", "makine" | sort: "order" %}
  {% include solution-list.html posts=makineler %}
</div>

<div class="page-section">
  <h2>Modül Çözümleri</h2>
  {% assign moduller = site.posts | where: "lang", "tr" | where: "categories", "modul" | sort: "order" %}
  {% include solution-list.html posts=moduller %}
</div>

<div class="page-section">
  <h2>Dokümantasyon</h2>
  {% assign dokumanlar = site.posts | where: "lang", "tr" | where: "categories", "dokumantasyon" | sort: "order" %}
  {% if dokumanlar.size == 0 %}
  <p>Yakında JumpCloud ve Trend Micro üzerine yazılar burada olacak. 🌸</p>
  {% else %}
  {% include solution-list.html posts=dokumanlar %}
  {% endif %}
</div>
