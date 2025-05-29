<div style="display: flex; align-items: center; justify-content: space-between; gap: 40px; flex-wrap: wrap; margin-top: 60px;">

  <!-- Sol taraf: Karşılama metni -->
  <div style="flex: 1; min-width: 250px;">
    <h1 style="font-size: 2.2em; margin-bottom: 12px;">Hoş geldin!</h1>
    <p style="font-size: 1.2em; line-height: 1.6;">
      Ben Naz. Siber güvenliği pembe odamdan öğreniyorum.<br>
      Burada çözdüğüm CTF’leri, öğrendiğim şeyleri ve küçük notlarımı paylaşıyorum.
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
