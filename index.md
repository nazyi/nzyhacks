<div style="display: flex; align-items: center; justify-content: space-between; gap: 32px; margin-top: 40px; flex-wrap: wrap;">

  <!-- Sol: Selamlama Metni -->
  <div style="flex: 1; min-width: 250px;">
    <h2 style="margin-bottom: 16px;">Selam! </h2>
    <p style="font-size: 1.2em;">Ben Naz. Siber güvenlik tutkunu, CTF meraklısı ve nzyhacks’in yaratıcısıyım.</p>
  </div>

  <!-- Sağ: Avatar Fotoğrafı -->
  <div style="flex: 1; min-width: 250px; text-align: center;">
    <style>
      .profile-photo {
        width: 200px; /* sabit boyut verelim ki daire net gözüksün */
        height: 200px;
        border-radius: 50%;
        object-fit: cover; /* resim taşmadan sığsın */
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        transition: transform 0.3s ease, box-shadow 0.3s ease;
      }

      .profile-photo:hover {
        transform: scale(1.05);
        box-shadow: 0 6px 18px rgba(0, 0, 0, 0.2);
      }
    </style>

    <img src="{{ '/assets/images/ben.png' | relative_url }}" alt="Naz" class="profile-photo">
  </div>

</div>

