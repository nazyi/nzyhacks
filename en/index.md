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
    <img src="{{ '/assets/images/waving.png' | relative_url }}" alt="Naz Avatar" class="avatar-photo">
  </div>
</div>

<div class="feature-grid">
  <div class="feature-card fade-in-left">
    <h3>CTF Adventures</h3>
    <p>You can find the machines I've solved on platforms like Hack The Box, TryHackMe, and CyberExam, along with the notes I took along the way.</p>
  </div>

  <div class="feature-card fade-in-right">
    <h3>What I'm Learning</h3>
    <p>I deepen my knowledge by working through different modules; you can find my notes and examples on this page.</p>
  </div>

  <div class="feature-card fade-in-left">
    <h3>Scratchpad</h3>
    <p>Sometimes small tips, sometimes command-line notes… This is where I jot down what I learn, try out, and discover.</p>
  </div>
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
