---
categories: [makine]
layout: post
title: TryHackMe Pickle Rick
desc: "Rick and Morty temalı bu görev, bir web sunucusunu istismar etmenizi ve Rick'in iksirini yapmasına ve kendini bir turşudan insana dönüştürmesine yardımcı olacak üç malzemeyi bulmanızı gerektiriyor."
logo: "/assets/images/picklerick.jpeg"
author: Buse Naz Yılmaz
---
# Port Taraması

Bizden Rick’i tekrardan insana çevirmek için gereken üç tane malzemeyi soruyor.

Makine IP adresimiz: 10.10.246.186

Bilgi toplamak için nmap taraması yaparak başlıyorum.
<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> nmap -sC -sV 10.10.246.186<br>  
PORT   STATE SERVICE VERSION<br>  
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)<br>  
| ssh-hostkey:<br>  
|   3072 03:b8:cc:f9:aa:e4:d5:dd:cb:a7:e8:9c:22:1b:4a:5e (RSA)<br>   
|   256 b3:ac:ad:44:04:b9:3f:ee:b6:7a:9c:bc:19:c9:04:86 (ECDSA)<br>   
|_  256 7c:06:dd:f0:cd:4f:6f:05:ef:94:d7:81:21:67:e5:12 (ED25519)<br>  
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))<br>  
|_http-title: Rick is sup4r cool<br>  
|_http-server-header: Apache/2.4.41 (Ubuntu)<br>  
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel<br>    
</div>
Nmap taraması sonucunda ssh ve http portlarının açık olduğunu buluyoruz. SSH hakkında elimizde açık bir zafiyet olmadığı için 80 portuna tarayıcı üzerinden erişiyorum. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/first.webp" width="500" height="400">
</div>

Rick bizden bilgisayarına erişip son üç tane gizli malzemeyi bulmamızı istiyor fakat şifresini hatırlamadığını belirtiyor. Web sayfası üzerinden bilgi edinmye çalışalım. İlk öncelikle sayfanın kodunu incelemeyle başlayalım. Kaynak kodunu incelerken bize verilen bir kullanıcı adı olduğunu görüyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/sec.webp" width="700" height="400">
</div>

Harika! Şimdi ise daha fazla detay öğrenmek için gizli dosyaları tarayacağız.

# Dosya Tarama

Bu işlem için gobuster isimli bir aracı kullanacağız. Gobuster, hızlı ve güçlü brute-force kullanarak dizin ve dosya bulma tarayıcısıdır. Bu aracı kullanmak için aşağıdaki komutu kullancağız.

<div class="code-window">
<br>
<span class="highlight">nzy@kali$</span> gobuster dir -u http//10.10.246.186 -w /root/Desktop/SecLists-master/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,sh,txt,cgi,html,css,js,py
</div>
Bu komut bizim -w parametresi ile belirttiğimiz wordlist ögelerini deneyerek gizli dosyaları bulmamızı sağlayacak.  Komutun çıktısında birkaç tane gizli dosya bulabildiğimizi görüyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/th.webp" width="650" height="100">
</div>

Bu dosyaları tarayıcı üzerinde görüntüleyelim. İlk olarak login.php adresine gidelim. Adreste aşağıdaki ekran görüntüsü gibi bir giriş sayfası bizi karşılıyor. 
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/fort.webp" width="380" height="440">
</div>

Bir kullanıcı adına sahibiz fakat şifreyi hala bilmiyoruz. Gobuster bize diğer birkaç tane dosya daha olduğunu söylemişti. O dosyadan bir tanesi de robots.txt (çıktının aşağılarında olduğu için ekran görüntüsünde yer almıyor). Robots.txt dosyası, Google botlarına hangi sayfaları ve dizinleri tarayıp indekslenebileceklerini hangilerini taramayacaklarını bildiren bir sayfadır. 
Bu sayfada bize bir değer veriliyor. 

<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/fif.webp" width="400" height="100">
</div>
# İlk Malzeme

Bu değeri giriş yaparken şifre olarak deneyelim. Bingo! Giriş yapabildik. Bizi bir command panel karşılıyor.
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/si.webp" width="500" height="100">
</div>
Panel üzerinde ls komutu ile listeleme yapalım. 
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/seve.webp" width="200" height="200">
</div>
İlk dosyanın adı oldukça şüpheli gözüküyor. Dosyaya erişmek için [http://10.10.246.186/Sup3rS3cretPickl3Ingred.txt](http://10.10.246.186/Sup3rS3cretPickl3Ingred.txt) isimli URL adresine gidelim.
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/ei.webp" width="500" height="100">
</div>
Bingo ilk gizli malzememizi buluyoruz. Daha fazla malzeme toplamak için devam edelim. Ls komutu ile bulduğumuz dosyalara tekrardan göz gezdirelim. Dosyaların arasından clue.txt dosyası ile bir ipucu yakalayabiliriz. 
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/nin.webp" width="400" height="100">
</div>
# İkinci Malzeme

Dosya sistemine göz atmamız gerektiğini söylüyor.

·        ls /home

 ile home klasörümüzün içini görüntüleyelim. Çıktıda rick ve ubuntu isimli iki farklı klasör grüyoruz. Bunlardan rick olanı görüntüleyelim.

·        ls /home/rick

Burada second ingredients isimli bir dosya olduğunu görüntülüyoruz. Fakat bu dosyanın içeriğini cat nano veya vim tarzı komutlarla görüntüleyemiyoruz.
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/ten.webp" width="300" height="180">
</div>
Cat benzeri komutları araştırıp şansımızı tekrardan deneyelim. Aşağıdaki komut ile çıktıya ulaşabiliyorum.  
·        less ‘/home/rick/second ingredients’
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/el.webp" width="150" height="50">
</div>
Diğer malzemeyi bulmak için araştırmamıza devam edelim.

# Üçüncü Malzeme

Root klasörünün içeriğini görüntülemeye çalışalım. ls /root komutunu deneyelim fakat sanırım root klasörüne erişimimiz yok. Yetkinliğimizi görüntülemek için sudo -l komutunu kullanalım. Fakat bu da ne?
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/twe.webp" width="750" height="100">
</div>
Çıktıda belirttiği şey www-data kullanıcısı herhangi bir komutu şifresiz olarak çalıştırabilir. O halde root klasörünün içini görüntüleyebiliriz.

·        sudo ls /root
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/13.webp" width="75" height="60">
</div>
Ve üçüncü malzememizin bulunduğu txt dosyasını görüyoruz. Less komutunu kulalanrak içeriğini görüntüleyelim ve son bayrağımızı da alalım.

·        less /root/3rd.txt
<div style="text-align: center;">
  <img src="./assets/images/tryhackme_picklerick/14.webp" width="250" height="50">
</div>
