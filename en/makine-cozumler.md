---
layout: default
title: Machine Write-ups
lang: en
permalink: /en/makine-cozumler
translation_url: /makine-cozumler
---

# Machine Write-ups

{% assign makineler = site.posts | where: "lang", "en" | where: "categories", "makine" | sort: "order" %}
{% include solution-list.html posts=makineler round=true %}
