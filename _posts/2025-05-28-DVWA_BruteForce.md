---
categories: [makine]
layout: post
desc: "DVWA (Damn Vulnerable Web Application) üzerindeki brute force zafiyet laboratuvarında, web uygulamalarına karşı kullanıcı adı ve şifre kombinasyonlarını otomatik araçlarla deneyerek kimlik doğrulama mekanizmalarını aşmayı öğrendik. Bu labda, Hydra gibi araçlar kullanarak zayıf veya tahmin edilebilir şifreleri nasıl tespit edebileceğimizi ve bir sisteme yetkisiz erişim sağlayabileceğimizi uygulamalı olarak gördük."
logo: "/assets/images/dvwa1.png"
author: Buse Naz Yılmaz
title: DVWA Brute Force
tags: [web] 
---

## Low Sec

### Character Set

Güvenlik seviyesi düşükte brüte force saldırısı denedim. İlk önce Burp üzerinde giden paketi yakaladım ve bunu Intruder’a gönderdim. Attack Type Spider olarak girdim. Payload Type ise Brute Force olarak girdim. Oynayacağım parametreler üzerinde işaretleme yaptıktan sonra character set ile denenilecek harf, sayı ve sembolleri girdim.

Kullanıcı adım admin şifrem ise password.

<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/lowsec1.webp" width="850" height="270">
</div>

### Dictionary Attack

Bu atakta ise olası kullanıcı adlarını ve şifrelerini ayrı olarak bir txt dosyası içerisine yazıp payload list olarak Burp’e yüklüyoruz. Txt dosyası oluşturmak için kodlar aşağıdadır:

·        nano olasinick.txt

·        nano olasisifre.txt

Bu sefer Attack Type Cluster Bomb seçtim. Yine deneme yapacağım parametreler üzerinde işaretlemeler yaptım. 2 tane parametremiz olduğu için hangi parametrede hangi payload dosyasını kullanacaksam Payload List kısmından ona göre seçtim. Örnek olarak ilk parametrem username ise Payload List 1 seçip Load butonundan olasinick.txt seçtim. Payload Type Simple list’te kaldı. Settings ayarlarına gelip Grep - Match bölümünde olan listeyi clear ile temizledikten sonra incorrect ekledim. Bunu eklememin sebebi doğru giriş yaptığımda anlamam için bir işaret olması gerekiyordu. Her denemede gelen password is incorrect hatasını burp algılayıp olanları 1 olmayanları 0 olarak sınıflandırdığı için doğru girişimdeki değerleri direkt seçebilecektim.

<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/cluster.webp" width="850" height="270">
</div>

<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/grep.webp" width="560" height="470">
</div>

Aşağıdaki çıktıda değerler işaretlenmiştir. 
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/adminpass.webp" width="800" height="250">
</div>

## Wfuzz

Bütün user’ları bulmak için [http://localhost./hackable/users/](http://localhost./hackable/users/) adresine gidelim. Buradaki kullanıcı isimlerini bir txt dosyasına kaydedelim işimizi kolaylaştırması için. Aşağıdaki wfuzz komutunu kullanarak

·        wfuzz --hs "Username and/or password incorrect." -c -z file,olasinick.txt -z file,rockyou.txt -b 'security=low; PHPSESSID=0gdtua47fc647dgjj7sitbqaa1' 'http://localhost./vulnerabilities/brute/index.php?username=FUZZ&password=FUZ2Z&Login=Login' | grep -v '250'

bütün userların şifrelerini deneyelim.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/target.webp" width="1000" height="180">
</div>
## Medium Sec

### Burp

Burada olayın trick kısmı kaynak kodları incelediğimizde gözüküyor. DVWA arayüzünde en altta view source üstüne tıklayıp view all dediğimizde her seviyenin kaynak kodunu görmekteyiz. Burada low ile medium arasındaki kaynak kod farklılıklarına bakarsak şunu fark edeceksiniz:
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/sleep.webp" width="750" height="150">
</div>
Buradaki sleep (2) kodu, kullanıcı her yanlış giriş yaptığında 2 saniye onu bekletmek demektir. Bunu genele vurduğumuzda ise brute-force atakları zaten uzun sürüyorken her denemede ekstra olarak 2 saniye bekletmek işi daha da zorlaştırır.

### Hydra

Hydra’da brute-force yapmak için komutumuz şu şekilde:
<div class="code-window">
<br>
<span class="highlight">root@kali$</span> hydra -l admin -P /root/Desktop/olasisifre.txt 127.0.0.1 http-get-form "/vulnerabilities/brute/:username=^USER^&password=^PASS^&user_token=%CSRF%&Login=Login:H=Cookie: PHPSESSID=hdbj798bma7cpkjsdr42ja8r73; security=medium:F=Username and/or password incorrect." -t 6 -v
</div>
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/hydra.webp" width="850" height="270">
</div>
##  High Sec

Yüksek seviyede kaynak kodu incelediğimizde brute-force atağını engellemek amaçlı anti-csrf token kullanıldığı görülmüştür. Peki nedir bu anti- csrf token, ne işe yarar?

Anti-CSRF token, CSRF saldırılarına karşı koruma sağlayan rastgele üretilmiş bir değerdir. Kullanıcı her istek yaptığında bu token form verisi veya header ile gönderilir. Sunucu, gelen token'ı kendi sakladığı değerle karşılaştırarak isteğin yetkili olduğunu doğrular. Token eşleşmezse istek reddedilir, böylece yetkisiz işlemler engellenir.

Gelelim Burp üzerinde bu işlemi nasıl gerçekleştirdiğimize. İlk öncelikle paketi yakalıyoruz random bir deneme yapıp. Ondan sonra sağ üstte bulunan ayarlar kısmından Session sekmesine geliyoruz. Session handling rules kısmından add diyoruz.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/session.webp" width="1050" height="255">
</div>
Rule actions kısmından Run macro seçeneğini seçiyoruz. Run Macro, oturum açma veya token yenileme gibi otomatik işlemleri tekrar ederek isteklere dinamik değerlerin eklenmesini sağlar.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/runmacro.webp" width="500" height="320">
</div>
Select Macro kısmından add dedikten sonra aşağıdaki Tolerate URL mismatch kabul ediyoruz. Bu özellik, parametreleri eşleştirirken URL farklılıklarını göz ardı ederek aynı parametre adlarına sahip isteklerin eşleşmesine izin verir. Özellikle oturum doğrulama veya token yenileme gibi işlemlerde farklı URL'ler arasında parametrelerin takibini kolaylaştırır.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/addmacro.webp" width="700" height="400">
</div>
Add ile macro paketimizi yükledikten sonra Configure Item üzerine tıklıyoruz.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/configure.webp" width="850" height="80">
</div>
Configure Item içinde aşağıda bulunan custom parameter bölümüne add diyoruz. Açılan sayfada parameter adını yazıp en altta bulunan search yerine token diyip aratıyoruz. Çıkan sonuçta token değerini alıyoruz. OK’a basıp kapatıyoruz.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/macroitem.webp" width="860" height="490">
</div>
Yine Session handling rule editör sayfasına gelince bu sefer Scope sekmesinden Tools Scope üzerinde sadece Intruder’ı tikli bırakıp URL Scoper üzerinden ise Use Suite Scope işaretliyoruz.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/tool.webp" width="855" height="400">
</div>
Her şey bitince Intruder’a gelip paketimiz üzerinden işlemlerimizi tekrardan yapıyoruz.
<div style="text-align: center;">
  <img src="./assets/images/dvwa_bruteforce/son.webp" width="850" height="230">
</div>
