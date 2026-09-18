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
{% include solution-list.html posts=dokumanlar dark_card=true %}
{% endif %}
