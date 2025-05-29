<div style="display: flex; align-items: center; justify-content: space-between; gap: 40px; flex-wrap: wrap; margin-top: 60px;">

  <!-- Sol taraf: Karşılama metni -->
  <div style="flex: 1; min-width: 250px;">
    <h1 style="font-size: 2.2em; margin-bottom: 12px;">Hoş geldin!</h1>
    <p style="font-size: 1.2em; line-height: 1.6;">
    Ben Naz. Siber güvenlik yolculuğumu burada belgeliyorum; öğrendiklerimi ve deneyimlerimi paylaşmak için kendi küçük köşem.
    </p>
  </div>

  <!-- Sağ taraf: Selamlayan avatar -->
  <div style="flex: 1; min-width: 250px; text-align: center;">
    <style>
      .waving-avatar {
        width: 220px;
        height: 220px;
        border-radius: 50%;
        object-fit: cover;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
        transition: transform 0.3s ease;
      }

      .waving-avatar:hover {
        transform: rotate(3deg) scale(1.05);
      }
    </style>
    <img src="{{ '/assets/images/waving.png' | relative_url }}" alt="Naz Avatar" class="waving-avatar">
  </div>
</div>

<!-- Altına Eklenen Kartlar -->
<div style="display: flex; flex-direction: column; gap: 40px; margin-top: 80px; padding: 0 20px;">
  <style>
    .card {
      background-color: #1e1e1e;
      color: #eee;
      padding: 24px;
      border-radius: 16px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      opacity: 0;
      transform: translateY(40px);
      transition: all 0.8s ease;
      max-width: 800px;
      min-width: 800px;
      margin: 0 auto;
    }

    .fade-in-left {
      transform: translateX(-100px);
    }

    .fade-in-right {
      transform: translateX(100px);
    }

    .card.visible {
      opacity: 1;
      transform: translateX(0);
    }
  </style>

  <div class="card fade-in-left">
    <h3>CTF Maceralarım</h3>
    <p>Hack The Box, TryHackMe, CyberExam gibi platformlarda çözdüğüm makineleri ve edindiğim notları buradan görebilirsin.</p>
  </div>

  <div class="card fade-in-right">
    <h3>Öğrendiklerim</h3>
    <p>Farklı modüller üzerinde çalışarak bilgimi derinleştiriyorum; bu sayfada notlarımı ve örnekleri bulabilirsin.</p>
  </div>

  <div class="card fade-in-left">
    <h3>Karalama Defteri</h3>
    <p>Bazen küçük ipuçları, bazen komut satırı notları… Burada öğrendiklerimi, denediklerimi ve bulduklarımı karalıyorum.</p>
  </div>
</div>

<!-- Odamın Fotoğrafı ve Yazı Bölümü -->
<div style="display: flex; align-items: center; justify-content: center; flex-wrap: wrap; margin-top: 100px; gap: 40px; padding: 0 20px;">
  <!-- Sol: Oda Fotoğrafı -->
  <div style="flex: 1; min-width: 250px; text-align: center;">
    <img src="{{ '/assets/images/odam.jpg' | relative_url }}" alt="Naz'ın Odası" style="width: 100%; max-width: 400px; border-radius: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.2);">
  </div>

  <!-- Sağ: Yazı -->
  <div style="flex: 1; min-width: 250px;">
    <h2 style="font-size: 1.8em; margin-bottom: 12px;">İşlerin piştiği yer 😼</h2>
    <p style="font-size: 1.2em; line-height: 1.6; color: #ddd;">
      Aile bütçesiyle ters orantılı ama hayallerimle doğru orantılı bir köşe. 
    </p>
  </div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    const cards = document.querySelectorAll('.card');

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
