---
categories: [modul]
layout: post
description: "Cisco Ethical Hacker kursunun dördüncü bölümüdür. Sosyal mühendislik saldırılarını (pretexting, e-posta phishing, tabnabbing vb.) ve BeEF ile DVWA üzerinden uygulamalı örnekleri ele alır."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Modül 4
tags: [Cisco, Sosyal Mühendislik]
order: 6
translation_url: /en/Cisco_Module4
---

## Cisco Ethical Hacker

## Module 4: Social Engineering Attacks

### 4.1 Pretexting for an Approach and Impersonation

Sosyal mühendislikte adı geçen bazı terimleri açıklayayım.

·        **Pretexting**: Ön metin oluşturma

·        **Impersonation**: Kimliğe bürünme, örnek olarak BT elemanı gibi davranmak.

·        **Pharming**: Sahte siteyi gerçekmiş gibi gösterip kullanıcıyı siteye yönlendirmek.

### 4.2 Social Engineering Attacks

#### 4.2.1 Email Phishing

Phishing saldırısında, saldırgan kullanıcıya güvenilir ve geçerli gibi bir site gönderip bilgilerini girmesini ister.

**Spear Phishing**

Phishing’in kişiye özel veya belirli şirket gruplarına yönelik yapılan oltalamadır.

**Whaling**

Temelde phishing ve spear phishing ile benzerdir fakat hedef olarak üst düzey yöneticiler veya önemli insanlardır.

#### 4.2.2 Vishing

Bir telefon görüşmesi üzerinden gerçekleştirilen sosyal mühendislik saldırısıdır. Hedefin çeşitli bilgilerini elde etmeye çalışır.

#### 4.2.3 Short Message Service (SMS) Phishing

Mobil cihazlara gelen kısa mesajlar ile çeşitli phishing yöntemleri de mevcuttur. Bir ödül kazandınız, amazon siparişinizle ilgili bir sorun var vb. içeriklere sahip olabilirler.

#### 4.2.4 Universal Serial Bus (USB) Drop Key

Saldırganların bir başka taktiği de zararlı yazılımlar içeren USB’leri olur olmadık yerlerde bırakmaktır. İnsanlar tereddüt etmeden yerden buldukları USB’leri kendi bilgisayarlarına takmaktadırlar.

#### 4.2.5 Watering Hole Attacks

Saldırgan, hedef kullanıcının düzenli olarak ziyaret ettiği web sitelerini analiz eder ve kod enjekte etmeye çalışır. Böylece kurban bir sonraki ziyaretinde kod çalışır ve başka kötü amaçlı bir siteye yönlendirilir. Bu yönlendirme türü aynı zamanda **pivot saldırısı** olarak da bilinir.

### 4.3 Physical Attacks

#### 4.3.1 Tailgating

Piggybacking yetkili kişinin izni dahilinde kısıtlı bir alana girmesiyle gerçekleşir. Yani örnek verecek olursak biri içeri girerken başka birinin ona kapıyı tutar mısınız demesi piggybacking’dir.

Tailgating ise yetkili bir kişinin izi olmadan insanlardan gizlice içeri girmeye denir.

#### 4.3.2 Dumpster Diving

Saldırgan, hedef kişinin çöplerini karıştırarak kişi hakkında bilgi toplamaya çalışır.

#### 4.3.3 Shoulder Surfing

Kişinin izni olmadan kişinin omzu üzerinden laptop veya telefonundan yazı yazarken bakıp kişisel bilgilerini öğrenmektir.

#### 4.3.4 Badge Cloning

Kurumda çalışan kişilerin rozet veya kartlarını klonlayarak çoğaltılması işlemine denir.

### 4.4 Social Enginerring Tools

#### 4.4.1 Social-Engineer Toolkit (SET)

SET kullanarak spear phing emailinin ne kadar kolay yapıldığını görelim.

**Step 1**

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo setoolkit
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/fsoci.webp' | relative_url }}" width="300" height="500" alt="Terminalde sudo setoolkit komutunun çalıştırılması">
</div>

**Step 2**

Menü üzerinden Social-Engineering Attack seçeneğini seçelim.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/socialeng.webp' | relative_url }}" width="500" height="250" alt="SET menüsünde Social-Engineering Attacks seçeneğinin seçilmesi">
</div>

**Step 3**

Çıkan menü üzerinden de Spear-Phishing Attack Vectors seçeneğini seçelim.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/spearp.webp' | relative_url }}" width="500" height="250" alt="Spear-Phishing Attack Vectors menü seçeneğinin görünümü">
</div>

**Step 4**

Burada bize yine birkaç tane seçenek sunuluyor biz 2. Seçeneği seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/createf.webp' | relative_url }}" width="400" height="100" alt="Spear-phishing saldırısı için dosya oluşturma seçeneğinin seçilmesi">
</div>

**Step 5**

Burada file formatı seçmemiz isteniliyor. Biz 13. Seçenekten devam ediyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/adobe.webp' | relative_url }}" width="600" height="460" alt="Zararlı PDF için dosya formatı seçeneklerinin listesi">
</div>

**Step 6**

E-maile koyacağımız PDF dosyasının formatının nasıl olduğunu seçiyoruz. Boş pdf seçeneği olan 2.yi seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/built.webp' | relative_url }}" width="600" height="70" alt="Boş PDF şablonu seçeneğinin seçilmesi">
</div>

**Step 7**

Hangi tür reverse Shell kullanacağımızı seçiyoruz. Biz ilk seçeneği seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/reverse.webp' | relative_url }}" width="1000" height="150" alt="Reverse shell payload türü seçim listesi">
</div>

**Step 8 – 9**

Shellin dinleme yapacağı IP adresi ve portu da verdikten sonra dosyanın adını değiştirmeyi veya değiştirmemeyi soruyor.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/setpayload.webp' | relative_url }}" width="640" height="450" alt="Dinleyici IP ve port bilgisinin girilmesi ve dosya adı sorusu">
</div>

**Step 10**

Bu zararlıyı bir e-mail grubuna mı yoksa tek bir e-mail adresine mi gönderileceğini belirliyoruz. Tek bir adresi seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/email.webp' | relative_url }}" width="600" height="130" alt="Zararlı dosyanın tek bir e-posta adresine gönderilme seçimi">
</div>

**Step 11 – 14**

E-mailin içeriğini oluşturduktan sonra mail gönderime hazır.

#### 4.4.2 Browser Exploitation Framework (BeEF)

XSS saldırısını kullanarak kullanıcı farklı kötü bir siteye yönlendirilerek çerezlerini çalmaya çalışır.

Browser Exploitation Framework ile XSS açıklarını kullanarak çerez çalmaya çalışılır.

Çalınan cookielerin örnek görüntüsü aşağıdadır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/cookie1.webp' | relative_url }}" width="650" height="600" alt="BeEF ile XSS üzerinden çalınan çerezlerin ekran görüntüsü">
</div>
Cookie çalındıktan sonra kullanıcıya fake bildirim bile gönderilebilmektedir. 

#### 4.4.3 Call Spoofing Tools

Arayan kişi olarak görünen numarayı çok basit bir şekilde değiştirebilirsiniz. Buna birkaç örnek tool verecek olursak:

·        **SpoofApp**: Hem Android hem iOS üzerinde numara spooflamak için kullanılan bir uygulamadır.

·        **SpoofCard**: Bu tool da hem Android hem de iOS üzerinde numara spooflamak, ses değiştirmek, farklı arka plan sesi oluşturmak için kullanılan bir uygulamadır.

·        **Arterisk**: Voice over IP kontrol aracıdır.

#### 4.4.4 Lab – Explore the Social Engineer Toolkit (SET)

##### Part 1 Cloning a Website to Obtain User Credentials

**Step 1: Investigate Web Attack Vectors in SET**

Setoolkit aracının menüsünden ilk başta “Social-Engineering Attacks” seçeneğini seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/social2.webp' | relative_url }}" width="420" height="180" alt="SET menüsünde Social-Engineering Attacks seçeneğinin seçilmesi">
</div>
Bu menüden sonra ise 2. seçenek olan “Website Attack Vectors” seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/website.webp' | relative_url }}" width="420" height="270" alt="Website Attack Vectors menü seçeneğinin seçilmesi">
</div>

Buradaki atakların açıklamasını okuduktan sonra bizim yapacağımız atak için 3. Seçenek olan “Credential Harvester Attack Method” seçiyoruz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/credential.webp' | relative_url }}" width="500" height="200" alt="Credential Harvester Attack Method seçeneğinin seçilmesi">
</div>

**Step 2: Clone the DVWA.vm login screen**

Bu adımda DVWA.vm oturum açma web sitesini kopyalacağız. SET bilgisayarda barındılan bir web sitesi oluşturur. Kurbanlar buraya bilgilerini girerse istismar edilecek.

Aşağıdaki menüden Site Cloner seçeneğini seçiyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/site.webp' | relative_url }}" width="300" height="120" alt="Site Cloner seçeneğinin menüden seçilmesi">
</div>
Bize web saldırganının IP adresini soruyor Kali makinemizde 10.6.6.0/24 bloğunda olduğumuz için 10.6.6.1 adresini giriyoruz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/podt.webp' | relative_url }}" width="800" height="20" alt="Saldırgan IP adresi olarak 10.6.6.1 girilmesi">
</div>

Şimdi ise klonlamak istediğimiz web sitesinin URL adresini giriyoruz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/createf.webp' | relative_url }}" width="400" height="10" alt="Klonlanacak DVWA web sitesinin URL adresinin girilmesi">
</div>

Başarılı bir şekilde dinlemeye başladık.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/webattack.webp' | relative_url }}" width="500" height="160" alt="Klonlanmış sitede dinlemenin başarıyla başladığını gösteren çıktı">
</div>

##### Part 2 Capturing and Viewing User Credentials

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
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa1.webp' | relative_url }}" width="530" height="450" alt="SET ile klonlanmış sahte DVWA giriş sayfasının görünümü">
</div>

Aşağıdaki ise orijinal sayfadır sayfanın uzantılarına dikkat edelim.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa2.webp' | relative_url }}" width="530" height="450" alt="Orijinal DVWA giriş sayfasının ve URL uzantısının görünümü">
</div>

Şimdi ise bilgilerimizi girerek test edelim. Aşağıdaki bilgileri girelim.

·        Username: [some.user@gmail.com](mailto:some.user@gmail.com)

·        Password: Pa55w0rdd!

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa3.webp' | relative_url }}" width="530" height="450" alt="Sahte DVWA sayfasına kullanıcı adı ve şifre girilmesi">
</div>

Login butonuna tıkladığımız an bizi dvwa sayfasının orijinaline yönlendirecek. Bunu sayfanın URL’sinden takip edebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/dvwa4.webp' | relative_url }}" width="530" height="450" alt="Giriş sonrası orijinal DVWA sayfasına yönlendirilmiş görünüm">
</div>

Yukarıda görüldüğü gibidir.

**Step 3: View the Captured Information**

SET aracının terminaline geri dönelim. Çıktıda girilen bilgileri görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/username.webp' | relative_url }}" width="730" height="150" alt="SET terminalinde yakalanan kullanıcı adı ve şifre çıktısı">
</div>

CTRL + C ile XML formatında bir rapor oluşturup kaydedebilirsiniz. Kaydedilen dosyaya cat ile erişerek içeriğini görüntüleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/cat.webp' | relative_url }}" width="530" height="450" alt="Cat komutuyla görüntülenen XML formatındaki yakalama raporu">
</div>

#### 4.4.5 Lab – Using the Browser Exploitation Famework (BeEF)

##### Part 1 Load the BeEF GUI Environment

**Step 1: Start BeEF**

Application> All Application> beef start menüsünden aracımızı çalıştıralım. İlk çalıştırdığımızda bizden şifreyi değiştirmemizi isteyecektir. Şifreyi değiştirin ve unutmayın.

GUI açıldıktan sonra bilgilerimizle giriş yapıyoruz.

·        Username: beef

·        Password: şifreniz

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/beef1.webp' | relative_url }}" width="450" height="370" alt="BeEF kontrol paneli giriş ekranı">
</div>

**Step 2: Hook the local browser to simulate a client-side attack**

Sömürmeden önce ilk olarak hedef tarayıcıyı “hook” etmeniz gerekir. Bu lab için yerel sistemi kullanacağız. Eğer gerçek bir test olsaydı kurbanın sık ziyaret ettiğin web istelerini belirleyip içine BeEF hook JavaScript kodu yerleştirip işlemi gerçekleştirirdik. Bu labda demo sürüm üzerinden gideceğiz.

Demo sürüm için bir websitesi oluşturulmuş bize.

[http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html)

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/beef2.webp' | relative_url }}" width="720" height="370" alt="BeEF hook demo sitesi butcher sayfasının görünümü">
</div>

Adresi üzerinden siteye erişebiliriz. Siteye eriştikten sonra biraz inceleyelim. Hook oluşturmak için arkda bir JS kodu çalıştığını biliyoruz. CTRL + U yaparak source code inceleyelim. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/script.webp' | relative_url }}" width="950" height="100" alt="Sayfa kaynak kodunda hook.js script referansının görünümü">
</div>

Burada yer alan hook.js dosyası ile beef hook oluşturduğumuzu görüyoruz. 
Kontrol panelinin olduğu sayfaya geri dönelim. Burada solda yer alan Hooked Browsers menüsü üzerinde yeni bilgiler eklendiğini görüyoruz.  

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/online.webp' | relative_url }}" width="300" height="200" alt="BeEF panelinde Hooked Browsers menüsünde yeni hedefin görünmesi">
</div>

Online Browsers menüsüne tıklıyoruz ve bilgiler önümüze geliyor. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/online2.webp' | relative_url }}" width="620" height="570" alt="BeEF Online Browsers menüsünde hooklanmış tarayıcı bilgileri">
</div>

##### Part 2 Investigate BeEF Exploit Capabilities

**Step 1: Investigate the commands and network tabs**

Diğer menüler hakkında da bilgi sahibi olalım. Commands menüsüne tıklayarak incelemeye başlayalım.

Burada yer alan Module Tree tarayıcıya yönelik gerçekletirebilecek tüm saldırı, bilgi toplama ve sosyal mühendislikleri kategorilere ayırmış şekilde gösterir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/browser.webp' | relative_url }}" width="500" height="330" alt="BeEF Commands sekmesinde Module Tree kategorilerinin listesi">
</div>

Bu menü üzerindekileri genişletirsek her fonksiyonun yanındaki renk kodlarını fark edeceksiniz. Her renk kodunun farklı bir anlamı vardır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/renkkod.webp' | relative_url }}" width="200" height="600" alt="BeEF modüllerinin renk kodlarına göre listelenmiş görünümü">
</div>

·        **Yeşil**: Bu komut modülü hedefe karşı çalışıyor ve kullanıcıya görünmezdir.

·        **Turuncu**: Bu komu modülü hedefe karşı çalışıyor fakat kullanıcıya gözükebilir.

·        **Beyaz**: Bu komut modülü hedefe karşı doğrulanmış değil.

·        **Kırmızı:** Bu komut modülü kullanıcıya karşı kullanılamıyor.

**Not**: Module Tree aynı bir filtre gibi kullanılır ve burada arama yapabilirsiniz.

Network menüsüne gidelim. Burada kurban ile olan ağ topolojisini görebilirsiniz. Biz local üzerinde çalıştığımız için sadece bir ağ ve bir hostu gösterecektir. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/hooked.webp' | relative_url }}" width="400" height="240" alt="BeEF Network sekmesinde kurban ile ağ topolojisi görünümü">
</div>

**Step 2: Use BeEF to iniate a social enginerring attack**

Bu adımda kancalanmış web sayfasına sahte bir bildirim göndererek kullanıcıya zararlı bir plugin yükleteceğiz.

Commands menüsüne tıklayalım. Social Engineering kategorisine kadar aşağıya inelim. Burada yer alan Fake Notification Bar (Firefox) seçeneğini seçelim.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/fake.webp' | relative_url }}" width="350" height="340" alt="Social Engineering kategorisinde Fake Notification Bar modülünün seçilmesi">
</div>

Seçtikten sonra modülün çalışacağı URL ve bildirimin göndereceği mesaj sağ tarafta menü üzerinde görüntülenmektedir. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/fake2.webp' | relative_url }}" width="460" height="240" alt="Fake Notification Bar modülünün URL ve mesaj ayarları paneli">
</div>

URL’yi http://10.6.6.13 olarak değiştirin. Bu URL DVWA sanal sunucusunun oturum açma ekranına yönlendirir. URL, yerel olarak veya ağda bulunan herhangi bir web sayfasını işaret edebilir. Canlı ortamda bu klonlanmış bir site veya kötü bir script içeren sayfa da olabilir. 
Gönderilecek mesajı da “AdBlocker Security Extension is out of date. Install the new version now.” olarak değiştirelim. 
Execute butonuna basarak modülü çalıştırabiliriz. Butcher sayfasına geri dönünce uyarıyı görüntüleyebilirsiniz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/plugin.webp' | relative_url }}" width="660" height="100" alt="Hedef tarayıcıda görüntülenen sahte eklenti güncelleme uyarısı">
</div>

Install plug-in butonuna tıklayınca aşağıdaki ekran görüntüsündeki gibi bizim klonladığımız kötü içerikli olan DVWA giriş sayfasına yönlendirilmektedir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/login.webp' | relative_url }}" width="360" height="330" alt="Sahte eklenti uyarısı sonrası yönlendirilen klonlanmış DVWA giriş sayfası">
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
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/tabnab.webp' | relative_url }}" width="430" height="240" alt="TabNabbing modülünün genel ayar ekranı">
</div>

15 dakika yerine 1 yazın ve tarayıcınıza 1 dakikalığına dokunmayın. Normalde tarayıcıda açık olan site
<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/butcher.webp' | relative_url }}" width="750" height="440" alt="Tarayıcıda açık olan orijinal butcher demo sayfası">
</div>
Bu iken, aşağıdaki ise 1 dakika boyunca boşta bırakılınca yönlendirilen sitedir. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/secret.webp' | relative_url }}" width="510" height="480" alt="TabNabbing ile bir dakika sonra yönlendirilen sahte sayfa">
</div>

Ortadaki kutucuğa “This is my secret” yazalım. Sonra Control Panel sayfasından Logs menüsünde kutucuğa yazılan değeri görebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/thisismy.webp' | relative_url }}" width="810" height="200" alt="BeEF Logs menüsünde yakalanan This is my secret metni">
</div>

### 4.5 Methods of Influence

·        **Authority**: Sosyal mühendislikte hem özgüven hem de belki otorite gösterir.

·        **Scarcity and Urgency**: Aciliyet duygusunu arttırmak kurbanı manipüle etmek için kullanılan bir yöntemdir.

·        **Social Proof**: İnsanlar bir durum karşısında nasıl davranacağını bilemediğinde, başkalarının davranışlarını örnek almasıdır.

·        **Likeness**: İnsanların hoşlandıkları kişilerden daha kolay etkilendiği için güzel görünümlü hoş birini kullanmak daha çok işe yarar.

·        **Fear**: İnsanlar başlarına kötü bir şey gelecek düşüncesiyle endişeyle düşüncesiz hareketler sergileyebilir.
