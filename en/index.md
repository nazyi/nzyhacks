---
layout: default
title: Home
lang: en
permalink: /en/
translation_url: /
---

<div class="hero">
  <div class="hero-text">
    <h1>Welcome!</h1>
    <p>I'm Naz. This is where I document my journey in IT and cybersecurity — my own little corner for sharing what I learn and experience.</p>
  </div>

  <div class="hero-avatar">
    <img src="{{ '/assets/images/waving.webp' | relative_url }}" alt="Naz Avatar" class="avatar-photo">
  </div>
</div>

<div class="feature-grid">

  {% assign home_posts = site.posts | where: "lang", "en" %}

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'makine'" | size %}
  <a class="feature-card fade-in-left" href="{{ '/en/makine-cozumler' | relative_url }}">
    <h3>CTF Adventures</h3>
    <p>You can find the machines I've solved on platforms like Hack The Box, TryHackMe, and CyberExam, along with the notes I took along the way.</p>
    <span class="feature-card-meta">{{ n }} machine write-ups <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'modul'" | size %}
  <a class="feature-card fade-in-right" href="{{ '/en/modul-cozumler' | relative_url }}">
    <h3>What I'm Learning</h3>
    <p>I deepen my knowledge by working through different modules; you can find my notes and examples on this page.</p>
    <span class="feature-card-meta">{{ n }} module notes <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'dokumantasyon'" | size %}
  <a class="feature-card fade-in-left" href="{{ '/en/dokumantasyon' | relative_url }}">
    <h3>Documentation</h3>
    <p>Setup, configuration, and usage notes for enterprise tools like JumpCloud and Trend Micro.</p>
    <span class="feature-card-meta">{{ n }} docs <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'blog'" | size %}
  <a class="feature-card fade-in-right" href="{{ '/en/bloglar' | relative_url }}">
    <h3>Scratchpad</h3>
    <p>Sometimes small tips, sometimes command-line notes… This is where I jot down what I learn, try out, and discover.</p>
    <span class="feature-card-meta">{{ n }} posts <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>
</div>

<div class="page-section page-section-spaced">
  <h2>Latest Posts</h2>
  {% assign latest_posts = site.posts | where: "lang", "en" | slice: 0, 3 %}
  {% include solution-list.html posts=latest_posts %}
</div>

<div class="split-section">
  <div class="split-media">
    <img src="{{ '/assets/images/odam.jpg' | relative_url }}" alt="Naz's Room">
  </div>

  <div class="split-text">
    <h2>Where the magic happens 😼</h2>
    <p>A corner that's inversely proportional to the family budget, but directly proportional to my dreams.</p>
  </div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    const cards = document.querySelectorAll('.feature-card');

    function revealOnScroll() {
      const triggerBottom = window.innerHeight * 0.85;

      cards.forEach(card => {
        const cardTop = card.getBoundingClientRect().top;
        if (cardTop < triggerBottom) {
          card.classList.add('visible');
        }
      });
    }

    window.addEventListener('scroll', revealOnScroll);
    revealOnScroll();
  });
</script>
