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
    <img src="{{ '/assets/images/waving.png' | relative_url }}" alt="Naz Avatar" class="avatar-photo">
  </div>
</div>

<div class="feature-grid">
  <div class="feature-card fade-in-left">
    <h3>CTF Maceralarım</h3>
    <p>Hack The Box, TryHackMe, CyberExam gibi platformlarda çözdüğüm makineleri ve edindiğim notları buradan görebilirsin.</p>
  </div>

  <div class="feature-card fade-in-right">
    <h3>Öğrendiklerim</h3>
    <p>Farklı modüller üzerinde çalışarak bilgimi derinleştiriyorum; bu sayfada notlarımı ve örnekleri bulabilirsin.</p>
  </div>

  <div class="feature-card fade-in-left">
    <h3>Karalama Defteri</h3>
    <p>Bazen küçük ipuçları, bazen komut satırı notları… Burada öğrendiklerimi, denediklerimi ve bulduklarımı karalıyorum.</p>
  </div>
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
