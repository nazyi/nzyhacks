---
layout: default
title: Ana Sayfa
translation_url: /en/
---

<div class="hero">
  <div class="hero-text">
    <h1>Hoş geldin!</h1>
    <p>Ben Naz. IT ve siber güvenlik alanındaki yolculuğumu burada belgeliyorum; öğrendiklerimi ve deneyimlerimi paylaşmak için kendi küçük köşem.</p>
  </div>

  <div class="hero-avatar">
    <img src="{{ '/assets/images/waving.webp' | relative_url }}" alt="Naz Avatar" class="avatar-photo">
  </div>
</div>

<div class="feature-grid">

  {% assign home_posts = site.posts | where: "lang", "tr" %}

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'makine'" | size %}
  <a class="feature-card fade-in-left" href="{{ '/makine-cozumler' | relative_url }}">
    <h3>CTF Maceralarım</h3>
    <p>Hack The Box, TryHackMe, CyberExam gibi platformlarda çözdüğüm makineleri ve edindiğim notları buradan görebilirsin.</p>
    <span class="feature-card-meta">{{ n }} makine çözümü <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'modul'" | size %}
  <a class="feature-card fade-in-right" href="{{ '/modul-cozumler' | relative_url }}">
    <h3>Öğrendiklerim</h3>
    <p>Farklı modüller üzerinde çalışarak bilgimi derinleştiriyorum; bu sayfada notlarımı ve örnekleri bulabilirsin.</p>
    <span class="feature-card-meta">{{ n }} modül notu <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'dokumantasyon'" | size %}
  <a class="feature-card fade-in-left" href="{{ '/dokumantasyon' | relative_url }}">
    <h3>Dokümantasyon</h3>
    <p>JumpCloud ve Trend Micro gibi kurumsal araçların kurulum, yapılandırma ve kullanım notlarını burada topluyorum.</p>
    <span class="feature-card-meta">{{ n }} doküman <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>

  {% assign n = home_posts | where_exp: "p", "p.categories contains 'blog'" | size %}
  <a class="feature-card fade-in-right" href="{{ '/bloglar' | relative_url }}">
    <h3>Karalama Defteri</h3>
    <p>Bazen küçük ipuçları, bazen komut satırı notları… Burada öğrendiklerimi, denediklerimi ve bulduklarımı karalıyorum.</p>
    <span class="feature-card-meta">{{ n }} yazı <span class="feature-card-arrow" aria-hidden="true">→</span></span>
  </a>
</div>

<div class="page-section page-section-spaced">
  <h2>Son Yazılar</h2>
  {% assign latest_posts = site.posts | where: "lang", "tr" | slice: 0, 3 %}
  {% include solution-list.html posts=latest_posts %}
</div>

<div class="split-section">
  <div class="split-media">
    <img src="{{ '/assets/images/odam.jpg' | relative_url }}" alt="Naz'ın Odası">
  </div>

  <div class="split-text">
    <h2>İşlerin piştiği yer 😼</h2>
    <p>Aile bütçesiyle ters orantılı ama hayallerimle doğru orantılı bir köşe.</p>
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
