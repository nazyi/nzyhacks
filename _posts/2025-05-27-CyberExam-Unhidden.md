---
categories: [makine]
layout: post
title: CyberExam Uncovering Hidden SSID 
description: "Kapsamı belirlemek için, kablosuz ağ penetrasyon testinde wifi ağlarını bulmaya çalışıyorum. Ancak, bazı SSID değerlerinin gizli olduğunu keşfettim. Bu konuda bana yardımcı olabilir misiniz?"
logo: "/assets/images/hidden_wifi.png"
tags: [CyberExam, WiFi]
order: 5
author: nazy
translation_url: /en/CyberExam-Unhidden
platform: CyberExam
difficulty: Easy
topic: "Gizli SSID"
topic_desc: "SSID'yi gizlemek ağı görünmez yapmaz; ağ adı, cihazlar ağa bağlanırken yine de havada iletilir."
---

## Giriş

Görevimiz yukarıda belirtildiği gibi gizli bir SSID’yi bulmamız. Bunun için öncelikle makinemize web üzerinden bağlanıyoruz. Bağlandıktan sonra root kullanıcımıza “user” şifresi ile geçiyoruz.

Kablosuz ağ arayüzlerini görüntülemek için komutumuzu kullanıyoruz.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> iwconfig
</div>

Bu komutun çıktısında wlan0 arayüzünü görüntülüyoruz. Wlan0 arayüzünün mode ise manuel olarak managed şeklinde ayarlanmış.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/iwconfig.webp' | relative_url }}" width="600" height="200" alt="iwconfig komutunun wlan0 arayüzü managed mod çıktısı">
</div>

Arayüzümüzün adını öğrendiğimize göre arayüzü monitör moduna alabiliriz.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> airmon-ng start wlan0
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/airmon.webp' | relative_url }}" width="600" height="200" alt="airmon-ng start wlan0 komutunun monitör modu çıktısı">
</div>

Monitör moduna aldığımızı kontrol etmek için tekrardan iwconfig komutu ile görüntüleyebiliriz ve dikkat ederseniz monitör moduna aldığımız arayüzün sonuna “mon” eklenerek yeni ismi wlan0mon oldu.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/iw2.webp' | relative_url }}" width="600" height="200" alt="iwconfig çıktısında wlan0mon olarak değişen arayüz adı">
</div>

## Saldırı

Arayüzümüzün adını öğrendiğimize göre saldırı aşamasına geçebiliriz. Kullanacağımız aracın adı airodump-ng. Bu araç ile trafiği dinleyebilir ve bir pakete kaydedebiliriz. Komutumuzu girelim.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> airodump-ng wlan0mon
</div>

Komutu girdikten sonra bir süre bekliyoruz ki paketler aksın, biz de BSSID gibi değerleri yakalayalım.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/air2.webp' | relative_url }}" width="600" height="200" alt="airodump-ng wlan0mon komutunun yakaladığı BSSID listesi">
</div>

Komut bir süre çalıştıktan sonra bir BSSID değer yakalıyoruz. Bu değer etraftaki bir kablosuz erişim noktasına ait olan MAC adresidir. Bu adresimizi şimdi dinlemeye alacağız. Bulduğumuz BSSID değerini komuta vermek için –bssid parametresi, hangi kanal üzerindeyse o kanalı belirtmek için -c parametresini, çıktıyı bir dosyaya kaydetmek için -w parametresini kullanacağız.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> airodump-ng –bssid 0A:F6:14:E7:8A:6B -c 6 -w capture wlan0mon
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/airodump.webp' | relative_url }}" width="600" height="90" alt="Belirli BSSID ve kanal için airodump-ng dinleme çıktısı">
</div>

Saldırının başarılı olup olmadığını çıktıda sağ üstte yer alan [WPA handshake: 0A:F6:14:E7:8A:6B] ile anlayabilirsiniz. Bu dinlemenin başarılı olduğunu ve 4-way handshake yakalandığını gösterir. Bu terminalimizde bu BSSID değerini dinlemeye başladıktan sonra bu ağın ESSID değerine erişmek için bu ağa bağlı olan bir cihaza ağdan koparma yani deauth saldırısı gerçekleştireceğiz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/wpa_handshake.webp' | relative_url }}" width="600" height="200" alt="airodump-ng çıktısında yakalanan WPA handshake bildirimi">
</div>

Bir süre bekledikten sonra ağa bağlı olan cihazın MAC adresi aşağıdaki STATION kısmında beliriyor. Bu STATION değerini kullanarak ona bir deauth saldırısı gerçekleştireceğiz. Böylece cihaz tekrar ağa bağlanmak istediğinde ESSID değeri açık bir şekilde gönderilecek. 

## Deauth

Deauth saldırısı bir cihazı zorla ağdan koparmak demektir. Bu saldırıyı ise aireplay-ng aracı ile birlikte gerçekleştireceğiz. Bu aracın amacı belirli davranışlar oluşturmaya zorlamaktır.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> aireplay-ng –deauth 10 -a 0A:F6:14:E7:8A:6B -c 6 7E:F4:4D:D9:5B:31 wlan0mon
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/aireplay.webp' | relative_url }}" width="600" height="200" alt="aireplay-ng ile gerçekleştirilen deauth saldırısının çıktısı">
</div>

Airodump-ng ile dinlemeye devam ettiğimiz terminale döndüğümüzde en sağda ağın normalde gizli fakat bizim bulduğumuz ESSID değerini göreceksiniz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/cyberexa.webp' | relative_url }}" width="600" height="200" alt="Deauth sonrası airodump-ng'de ortaya çıkan gizli ESSID değeri">
</div>

Ben saldırıyı bir adım öteye götürmek istedim ve ağın şifresini de bulmak istedim. Daha önceden trafiği kaydettiğimiz capture-01.cap isimli dosya ile şifreyi kırmayı deneyebiliriz.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> aircrack-ng -w wordlist.txt -b 0A:F6:14:E7:8A:6B capture-01.cap
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/cyberexam_unhidden/şifre.webp' | relative_url }}" width="500" height="300" alt="aircrack-ng ile capture dosyasından kırılan WiFi şifresi">
</div>
