---
layout: default
title: Module Write-ups
lang: en
permalink: /en/modul-cozumler
translation_url: /modul-cozumler
---

# Module Write-ups

{% assign moduller = site.posts | where: "lang", "en" | where: "categories", "modul" | sort: "order" %}
{% include solution-list.html posts=moduller %}
