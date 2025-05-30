---
categories: [makine]
layout: post
title: CyberExam Uncovering Hidden SSID 
desc: "Kapsamı belirlemek için, kablosuz ağ penetrasyon testinde wifi ağlarını bulmaya çalışıyorum. Ancak, bazı SSID değerlerinin gizli olduğunu keşfettim. Bu konuda bana yardımcı olabilir misiniz?"
logo: "/assets/images/hidden_wifi.png"
tags: [CyberExam]
author: Buse Naz Yılmaz
---
# Giriş
Görevimiz yukarıda belirtildiği gibi gizli bir SSID’yi bulmamız. Bunun için öncelikle makinemize web üzerinden bağlanıyoruz.  Bağlandıktan sonra root kullanıcımıza “user” şifresi ile geçiyoruz.
Kablosuz ağ ara yüzlerini görüntülemek için komutumuzu kullanıyoruz.
·        iwconfig

Bu komutun çıktısında wlan0 ara yüzünü görüntülüyoruz. Wlan0 ara yüzünün mode ise manuel olarak managed şeklinde ayarlanmış.

<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/iwconfig.webp" width="600" height="200">
</div>
Ara yüzümüzün adını öğrendiğimize göre ara yüzü monitör moduna alabiliriz.

·        airmon-ng start wlan0
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/airmon.webp" width="600" height="200">
</div>
Monitor moda aldığımızı kontrol etmek için tekrardan iwconfig komutu ile görüntüleyebiliriz ve dikkat ederseniz monitör moduna aldığımız ara yüzün sonuna “mon” eklenerek yeni ismi wlan0mon oldu.
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/iw2.webp" width="600" height="200">
</div>

# Saldırı
Ara yüzümüzün adını öğrendiğimize göre saldırı aşamasına geçebiliriz. Kullanacağımız aracın adı airodump-ng. Bu araç ile trafiği dinleyebilir ve bir pakete kaydedebiliriz. Komutumuzu girelim.

·        airodump-ng wlan0mon

Komutu girdikten sonra bir süre bekliyoruz ki paketler aksın, biz de BSSID gibi değerleri yakalayalım.
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/air2.webp" width="600" height="200">
</div>
Komut bir süre çalıştıktan sonra bir BSSID değer yakalıyoruz. Bu değer etraftaki bir kablosuz erişimine ait olan MAC adresidir. Bu adresimizi şimdi dinlemeye alacağız. Bulduğumuz BSSID değerini komuta vermek için –bssid parametresi, hangi kanal üzerindeyse o kanalı belirtmek için -c parametresini, çıktıyı bir dosyaya kaydetmek için -w parametresini kullanacağız.

·        airodump-ng –bssid 0A:F6:14:E7:8A:6B -c 6 -w capture wlan0mon
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/airodump.webp" width="600" height="90">
</div>
Saldırının başarılı olup olmadığını çıktıda sağ üstte yer alan [WPA handshake: 0A:F6:14:E7:8A:6B] ile anlayabilirsiniz. Bu dinlemenin başarılı olduğunu ve 4-way handshake yakalandığını gösterir. Bu terminalimizde bu BSSID değerini dinlemeye başladıktan sonra bu ağın ESSID değerine erişmek için bu ağa bağlı olan bir cihaza ağdan koparma yani deauth saldırısı gerçekleştireceğiz. 
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/wpa_handshake.webp" width="600" height="200">
</div>
Bir süre bekledikten sonra ağa bağlı olan cihazın MAC adresi aşağıdaki STATION kısmında beliriyor. Bu STATION değerini kullanarak ona bir deauth saldırısı gerçekleştireceğiz. Böylece cihaz tekrar ağa bağlanmak istediğinde ESSID değeri açık bir şekilde gönderilecek. 

# Deauth
Deauth saldırısı bir cihazı zorla ağdan koparmak demektir. Bu saldıyı ise aireplay-ng aracı ile birlikte gerçekleştireceğiz. Bu aracın amacı belirli davranışlar oluşturmaya zorlamaktır.

·        aireplay-ng –deauth 10 -a 0A:F6:14:E7:8A:6B -c 6 7E:F4:4D:D9:5B:31 wlan0mon
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/aireplay.webp" width="600" height="200">
</div>
Airedump-ng ile dinlemeye devam ettiğimiz terminale döndüğümüzde en sağda ağın normalde gizli fakat bizim bulduğumuz ESSID değerini göreceksiniz. 
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/cyberexa.webp" width="600" height="200">
</div>
Ben saldırıyı bir adım öteye götürmek istedim ve ağın şifresini de bulmak istedim. Daha önceden trafiği kaydettiğimiz capture-01.cap isimli dosya ile şifreyi kırmayı deneyebiliriz.

·        aircrack-ng -w wordlist.txt -b 0A:F6:14:E7:8A:6B capture-01.cap
<div style="text-align: center;">
  <img src="./assets/images/cyberexam_unhidden/şifre.webp" width="500" height="300">
</div>
