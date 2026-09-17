---
layout: default
title: Bloglar
translation_url: /en/bloglar
---

# Bloglar

{% assign blog_posts = site.posts | where: "lang", "tr" | where_exp: "post", "post.categories contains 'blog'" %}
{% include solution-list.html posts=blog_posts %}
