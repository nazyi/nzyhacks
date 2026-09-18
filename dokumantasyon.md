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
{% include solution-list.html posts=dokumanlar %}
{% endif %}
