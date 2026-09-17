---
layout: default
title: Modül Çözümleri
translation_url: /en/modul-cozumler
---

# Modül Çözümleri

{% assign moduller = site.posts | where: "lang", "tr" | where: "categories", "modul" | sort: "order" %}
{% include solution-list.html posts=moduller %}
