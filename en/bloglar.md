---
layout: default
title: Blog
lang: en
permalink: /en/bloglar
translation_url: /bloglar
---

# Blog

{% assign blog_posts = site.posts | where: "lang", "en" | where_exp: "post", "post.categories contains 'blog'" %}
{% include solution-list.html posts=blog_posts %}
