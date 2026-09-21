---
layout: default
title: Dokümantasyon
translation_url: /en/dokumantasyon
---

# Dokümantasyon

Kurumsal araçlarla ilgili kurulum, yapılandırma ve kullanım notlarımı bu sayfada topluyorum.

{% assign dokumanlar = site.posts | where: "lang", "tr" | where: "categories", "dokumantasyon" | sort: "order" %}

{% if dokumanlar.size == 0 %}
<p>Yakında JumpCloud ve Trend Micro üzerine yazılar burada olacak. 🌸</p>
{% else %}
{% assign gruplar = dokumanlar | group_by: "tool" %}
{% assign grup_isimleri = gruplar | map: "name" %}
<div class="doc-tabs">
  <div class="doc-tab-buttons">
    {% for grup in gruplar %}
      <button type="button" class="doc-tab-btn{% if forloop.first %} active{% endif %}" data-tab="doc-tab-{{ grup.name | slugify }}">{{ grup.name }}</button>
    {% endfor %}
    {% unless grup_isimleri contains "Trend Micro" %}
      <button type="button" class="doc-tab-btn" data-tab="doc-tab-trend-micro">Trend Micro</button>
    {% endunless %}
  </div>
  <div class="doc-tab-content">
    {% for grup in gruplar %}
      <div class="doc-tab-panel{% if forloop.first %} active{% endif %}" id="doc-tab-{{ grup.name | slugify }}">
        {% include solution-list.html posts=grup.items %}
      </div>
    {% endfor %}
    {% unless grup_isimleri contains "Trend Micro" %}
      <div class="doc-tab-panel" id="doc-tab-trend-micro">
        <p>Yakında Trend Micro üzerine yazılar burada olacak. 🌸</p>
      </div>
    {% endunless %}
  </div>
</div>
{% endif %}
