---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun dördüncü bölümüdür. Zafiyet tarayıcılarının çalışma prensipleri, tarama türleri (authenticated, unauthenticated, stealth, compliance vb.) ve Kali Linux üzerinde Nmap ile GVM araçları kullanılarak yapılan zafiyet analizleri uygulamalı olarak ele alınmıştır. Ayrıca, tarama sonuçlarının analizinde dikkat edilmesi gereken noktalar ile CVE, CWE, CVSS gibi güvenlik kaynakları tanıtılmıştır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Ethical Hacker Modül 4
order: 6
---

# Cisco Ethical Hacker

# Module 4: Social Engineering Attacks

## 4.1 Pretexting for an Approach and Impersonation

Sosyal mühendislikte adı geçen bazı terimleri açıklayayım.

·        **Pretexting**: Ön metin oluşturma

·        **Impersonation**: Kimliğe bürünme, örnek olarak BT elemanı gibi davranmak.

·        **Pharming**: Sahte siteyi gerçekmiş gibi gösterip kullanıcıyı siteye yönlendirmek.

## 4.2 Social Engineering Attacks

### 4.2.1 Email Phishing

Phishing saldırısında, saldırgan kullanıcıya güvenilir ve geçerli gibi bir site gönderip bilgilerini girmesini ister.

**Spear Phishing**

Phishing’in kişiye özel veya belirli şirket gruplarına yönelik yapılan oltalamadır.

**Whaling**

Temelde phishing ve spear phishing ile benzerdir fakat hedef olarak üst düzey yöneticiler veya önemli insanlardır.

### 4.2.2 Vishing

Bir telefon görüşmesi üzerinden gerçekleştirilen sosyal mühendislik saldırısıdır. Hedefin çeşitli bilgilerini elde etmeye çalışır.

### 4.2.3 Short Message Service (SMS) Phishing

Mobil cihazlara gelen kısa mesajlar ile çeşitli phishing yöntemleri de mevcuttur. Bir ödül kazandınız, amazon siparişinizle ilgili bir sorun var vb. içeriklere sahip olabilirler.

### 4.2.4 Universal Serial Bus (USB) Drop Key

Saldırganların bir başka taktiği de zararlı yazılımlar içeren USB’leri olur olmadık yerlerde bırakmaktır. İnsanlar tereddüt etmeden yerden buldukları USB’leri kendi bilgisayarlarına takmaktadırlar.

### 4.2.5 Watering Hole Attacks

Saldırgan, hedef kullanıcının düzenli olarak ziyaret ettiği web sitelerini analiz eder ve kod enjekte etmeye çalışır. Böylece kurban bir sonraki ziyaretinde kod çalışır ve başka kötü amaçlı bir siteye yönlendirilir. Bu yönlendirme türü aynı zamanda **pivot saldırısı** olarak da bilinir.

## 4.3 Physical Attacks

### 4.3.1 Tailgating

Piggybacking yetkili kişinin izni dahilinde kısıtlı bir alana girmesiyle gerçekleşir. Yani örnek verecek olursak biri içeri girerken başka birinin ona kapıyı tutar mısınız demesi piggybacking’dir.

Tailgating ise yetkili bir kişinin izi olmadan insanlardan gizlice içeri girmeye denir.

### 4.3.2 Dumpster Diving

Saldırgan, hedef kişinin çöplerini karıştırarak kişi hakkında bilgi toplamaya çalışır.

### 4.3.3 Shoulder Surfing

Kişinin izni olmadan kişinin omzu üzerinden laptop veya telefonundan yazı yazarken bakıp kişisel bilgilerini öğrenmektir.

### 4.3.4 Badge Cloning

Kurumda çalışan kişilerin rozet veya kartlarını klonlayarak çoğaltılması işlemine denir.

## 4.4 Social Enginerring Tools

### 4.4.1 Social-Engineer Toolkit (SET)

SET kullanarak spear phing emailinin ne kadar kolay yapıldığını görelim.

**Step 1**

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo setoolkit
</div>

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/fsoci.webp" width="300" height="500">
</div>

**Step 2**

Menü üzerinden Social-Engineering Attack seçeneğini seçelim.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/socialeng.webp" width="500" height="250">
</div>

**Step 3**

Çıkan menü üzerinden de Spear-Phishing Attack Vectors seçeneğini seçelim.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/spearp.webp" width="500" height="250">
</div>

**Step 4**

Burada bize yine birkaç tane seçenek sunuluyor biz 2. Seçeneği seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/createf.webp" width="400" height="100">
</div>

**Step 5**

Burada file formatı seçmemiz isteniliyor. Biz 13. Seçenekten devam ediyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/adobe.webp" width="600" height="460">
</div>

**Step 6**

E-maile koyacağımız PDF dosyasının formatının nasıl olduğunu seçiyoruz. Boş pdf seçeneği olan 2.yi seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/built.webp" width="600" height="70">
</div>

**Step 7**

Hangi tür reverse Shell kullanacağımızı seçiyoruz. Biz ilk seçeneği seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/reverse.webp" width="1000" height="150">
</div>

**Step 8 – 9**

Shellin dinleme yapacağı IP adresi ve portu da verdikten sonra dosyanın adını değiştirmeyi veya değiştirmemeyi soruyor.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/setpayload.webp" width="640" height="450">
</div>

**Step 10**

Bu zararlıyı bir e-mail grubuna mı yoksa tek bir e-mail adresine mi gönderileceğini belirliyoruz. Tek bir adresi seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/email.webp" width="600" height="130">
</div>

**Step 11 – 14**

E-mailin içeriğini oluşturduktan sonra mail gönderime hazır.

### 4.4.2 Browser Exploitation Framework (BeEF)

XSS saldırısını kullanarak kullanıcı farklı kötü bir siteye yönlendirilerek çerezlerini çalmaya çalışır.

Browser Exploitation Framework ile XSS açıklarını kullanarak çerez çalmaya çalışılır.

Çalınan cookielerin örnek görüntüsü aşağıdadır.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/cookie1.webp" width="650" height="600">
</div>
Cookie çalındıktan sonra kullanıcıya fake bildirim bile gönderilebilmektedir. 

### 4.4.3 Call Spoofing Tools

Arayan kişi olarak görünen numarayı çok basit bir şekilde değiştirebilirsiniz. Buna birkaç örnek tool verecek olursak:

·        **SpoofApp**: Hem Android hem iOS üzerinde numara spooflamak için kullanılan bir uygulamadır.

·        **SpoofCard**: Bu tool da hem Android hem de iOS üzerinde numara spooflamak, ses değiştirmek, farklı arka plan sesi oluşturmak için kullanılan bir uygulamadır.

·        **Arterisk**: Voice over IP kontrol aracıdır.

### 4.4.4 Lab – Explore the Social Engineer Toolkit (SET)

#### Part 1 Cloning a Website to Obtain User Credentials

**Step 1: Investigate Web Attack Vectors in SET**

Setoolkit aracının menüsünden ilk başta “Social-Engineering Attacks” seçeneğini seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/social2.webp" width="420" height="180">
</div>
Bu menüden sonra ise 2. seçenek olan “Website Attack Vectors” seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/website.webp" width="420" height="270">
</div>

Buradaki atakların açıklamasını okuduktan sonra bizim yapacağımız atak için 3. Seçenek olan “Credential Harvester Attack Method” seçiyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/credential.webp" width="500" height="200">
</div>

**Step 2: Clone the DVWA.vm login screen**

Bu adımda DVWA.vm oturum açma web sitesini kopyalacağız. SET bilgisayarda barındılan bir web sitesi oluşturur. Kurbanlar buraya bilgilerini girerse istismar edilecek.

Aşağıdaki menüden Site Cloner seçeneğini seçiyoruz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/site.webp" width="300" height="120">
</div>
Bize web saldırganının IP adresini soruyor Kali makinemizde 10.6.6.0/24 bloğunda olduğumuz için 10.6.6.1 adresini giriyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/podt.webp" width="800" height="20">
</div>

Şimdi ise klonlamak istediğimiz web sitesinin URL adresini giriyoruz. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/createf.webp" width="400" height="10">
</div>

Başarılı bir şekilde dinlemeye başladık.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/webattack.webp" width="500" height="160">
</div>

#### Part 2 Capturing and Viewing User Credentials

Normal bir saldırıda bu web sitesini kurbana iletmek için link veya QR kod ile gönderilirdi. Ancak bu lab ortamında sadece bir html dokümanı oluşturarak websitesine yönlendirme yapacağız.

**Step 1: Create the Social Engineering Exploit**

HTML dosyamızı oluşturalım sonra aşağıda verilen html kodu içine yazalım.

 **<html>**

**<head>**

meta http-equiv="refresh" content="0; url=http://10.6.6.1/" 

**</head>**

**</html>**

Kodu yazdıktan sonra adını Great\_link.html koyalım ve kaydedelim.

**Step 2: Capture User Credentials**

HTML dosyasını kaydettikten sonra üstüne çift tıklayalım ve klonladığımız sayfa açılsın. Peki bu sayfanın orijinalinden farkı nedir? Hemen inceleyelim. İlk görüntü benim klonladığım sayfadır.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/dvwa1.webp" width="530" height="450">
</div>

Aşağıdaki ise orijinal sayfadır sayfanın uzantılarına dikkat edelim.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/dvwa2.webp" width="530" height="450">
</div>

Şimdi ise bilgilerimizi girerek test edelim. Aşağıdaki bilgileri girelim.

·        Username: [some.user@gmail.com](mailto:some.user@gmail.com)

·        Password: Pa55w0rdd!

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/dvwa3.webp" width="530" height="450">
</div>

Login butonuna tıkladığımız an bizi dvwa sayfasının orijinaline yönlendirecek. Bunu sayfanın URL’sinden takip edebilirsiniz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/dvwa4.webp" width="530" height="450">
</div>

Yukarıda görüldüğü gibidir.

**Step 3: View the Captured Information**

SET aracının terminaline geri dönelim. Çıktıda girilen bilgileri görebilirsiniz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/username.webp" width="730" height="150">
</div>

CTRL + C ile XML formatında bir rapor oluşturup kaydedebilirsiniz. Kaydedilen dosyaya cat ile erişerek içeriğini görüntüleyebilirsiniz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/cat.webp" width="530" height="450">
</div>

### 4.4.5 Lab – Using the Browser Exploitation Famework (BeEF)

#### Part 1 Load the BeEF GUI Environment

**Step 1: Start BeEF**

Application> All Application> beef start menüsünden aracımızı çalıştıralım. İlk çalıştırdığımızda bizden şifreyi değiştirmemizi isteyecektir. Şifreyi değiştirin ve unutmayın.

GUI açıldıktan sonra bilgilerimizle giriş yapıyoruz.

·        Username: beef

·        Password: şifreniz

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/beef1.webp" width="450" height="370">
</div>

**Step 2: Hook the local browser to simulate a client-side attack**

Sömürmeden önce ilk olarak hedef tarayıcıyı “hook” etmeniz gerekir. Bu lab için yerel sistemi kullanacağız. Eğer gerçek bir test olsaydı kurbanın sık ziyaret ettiğin web istelerini belirleyip içine BeEF hook JavaScript kodu yerleştirip işlemi gerçekleştirirdik. Bu labda demo sürüm üzerinden gideceğiz.

Demo sürüm için bir websitesi oluşturulmuş bize.

[http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html)

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/beef2.webp" width="720" height="370">
</div>

Adresi üzerinden siteye erişebiliriz. Siteye eriştikten sonra biraz inceleyelim. Hook oluşturmak için arkda bir JS kodu çalıştığını biliyoruz. CTRL + U yaparak source code inceleyelim. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/script.webp" width="950" height="100">
</div>

Burada yer alan hook.js dosyası ile beef hook oluşturduğumuzu görüyoruz. 
Kontrol panelinin olduğu sayfaya geri dönelim. Burada solda yer alan Hooked Browsers menüsü üzerinde yeni bilgiler eklendiğini görüyoruz.  

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/online.webp" width="300" height="200">
</div>

Online Browsers menüsüne tıklıyoruz ve bilgiler önümüze geliyor. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/online2.webp" width="620" height="570">
</div>

#### Part 2 Investigate BeEF Exploit Capabilities

**Step 1: Investigate the commands and network tabs**

Diğer menüler hakkında da bilgi sahibi olalım. Commands menüsüne tıklayarak incelemeye başlayalım.

Burada yer alan Module Tree tarayıcıya yönelik gerçekletirebilecek tüm saldırı, bilgi toplama ve sosyal mühendislikleri kategorilere ayırmış şekilde gösterir.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/browser.webp" width="500" height="330">
</div>

Bu menü üzerindekileri genişletirsek her fonksiyonun yanındaki renk kodlarını fark edeceksiniz. Her renk kodunun farklı bir anlamı vardır.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/renkkod.webp" width="200" height="600">
</div>

·        **Yeşil**: Bu komut modülü hedefe karşı çalışıyor ve kullanıcıya görünmezdir.

·        **Turuncu**: Bu komu modülü hedefe karşı çalışıyor fakat kullanıcıya gözükebilir.

·        **Beyaz**: Bu komut modülü hedefe karşı doğrulanmış değil.

·        **Kırmızı:** Bu komut modülü kullanıcıya karşı kullanılamıyor.

**Not**: Module Tree aynı bir filtre gibi kullanılır ve burada arama yapabilirsiniz.

Network menüsüne gidelim. Burada kurban ile olan ağ topolojisini görebilirsiniz. Biz local üzerinde çalıştığımız için sadece bir ağ ve bir hostu gösterecektir. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/hooked.webp" width="400" height="240">
</div>

**Step 2: Use BeEF to iniate a social enginerring attack**

Bu adımda kancalanmış web sayfasına sahte bir bildirim göndererek kullanıcıya zararlı bir plugin yükleteceğiz.

Commands menüsüne tıklayalım. Social Engineering kategorisine kadar aşağıya inelim. Burada yer alan Fake Notification Bar (Firefox) seçeneğini seçelim.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/fake.webp" width="350" height="340">
</div>

Seçtikten sonra modülün çalışacağı URL ve bildirimin göndereceği mesaj sağ tarafta menü üzerinde görüntülenmektedir. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/fake2.webp" width="460" height="240">
</div>

URL’yi http://10.6.6.13 olarak değiştirin. Bu URL DVWA sanal sunucusunun oturum açma ekranına yönlendirir. URL, yerel olarak veya ağda bulunan herhangi bir web sayfasını işaret edebilir. Canlı ortamda bu klonlanmış bir site veya kötü bir script içeren sayfa da olabilir. 
Gönderilecek mesajı da “AdBlocker Security Extension is out of date. Install the new version now.” olarak değiştirelim. 
Execute butonuna basarak modülü çalıştırabiliriz. Butcher sayfasına geri dönünce uyarıyı görüntüleyebilirsiniz. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/plugin.webp" width="660" height="100">
</div>

Install plug-in butonuna tıklayınca aşağıdaki ekran görüntüsündeki gibi bizim klonladığımız kötü içerikli olan DVWA giriş sayfasına yönlendirilmektedir.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/login.webp" width="360" height="330">
</div>

**Step 3: Use TabNabbing to display malicious website**

Kancalanmış bir tarayıcı sekmesi çok uzun süre boşta kalırsa farklı bir URL adresine yönlendiren bir fonksiyondur.

Yukarıda yaptığımız işlemleri tekrarlayalım.

·        Yeni bir mozilla sayfası açın.

·        Yeni bir sayfa üzerinden [http://127.0.0.1:3000/ui/authentication](http://127.0.0.1:3000/ui/authentication) açın.

·        Sisteme bilgilerinizkle giriş yapın.

**·**        Mozilla üzerinden [http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html) **adresine erişin.**

**·**        **BeEF kontrol paneli üzerinden Online Browsers menüsünden** **Command** **sekmesini açın.**

**·**        **Social Engineering** **kategorisinden** **TabNabbing** **seçin.**

Burada yine modülün genel ayarlamalarını görebilirsiniz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/tabnab.webp" width="430" height="240">
</div>

15 dakika yerine 1 yazın ve tarayıcınıza 1 dakikalığına dokunmayın. Normalde tarayıcıda açık olan site
<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/butcher.webp" width="750" height="440">
</div>
Bu iken, aşağıdaki ise 1 dakika boyunca boşta bırakılınca yönlendirilen sitedir. 

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/secret.webp" width="510" height="480">
</div>

Ortadaki kutucuğa “This is my secret” yazalım. Sonra Control Panel sayfasından Logs menüsünde kutucuğa yazılan değeri görebilirsiniz.

<div style="text-align: center;">
  <img src="./assets/images/ciscomodule4/thisismy.webp" width="810" height="200">
</div>

## 4.5 Methods of Influence

·        **Authority**: Sosyal mühendislikte hem özgüven hem de belki otorite gösterir.

·        **Scarcity and Urgency**: Aciliyet duygusunu arttırmak kurbanı manipüle etmek için kullanılan bir yöntemdir.

·        **Social Proof**: İnsanlar bir durum karşısında nasıl davranacağını bilemediğinde, başkalarının davranışlarını örnek almasıdır.

·        **Likeness**: İnsanların hoşlandıkları kişilerden daha kolay etkilendiği için güzel görünümlü hoş birini kullanmak daha çok işe yarar.

·        **Fear**: İnsanlar başlarına kötü bir şey gelecek düşüncesiyle endişeyle düşüncesiz hareketler sergileyebilir.
