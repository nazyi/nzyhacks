---
layout: default
title: Makine Çözümleri
translation_url: /en/makine-cozumler
---

# Makine Çözümleri

{% assign makineler = site.posts | where: "lang", "tr" | where: "categories", "makine" | sort: "order" %}
{% include solution-list.html posts=makineler round=true %}
