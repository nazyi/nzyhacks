---
categories: [modul]
layout: post
description: "Cisco Ethical Hacker kursunun dördüncü bölümünün ikinci parçasıdır. Browser Exploitation Framework (BeEF) ile tarayıcı kancalama, sahte bildirim ve TabNabbing saldırılarını uygulamalı olarak ele alır ve sosyal mühendislikte kullanılan ikna yöntemlerini özetler."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Modül 4 (2/2)
tags: [Cisco, Sosyal Mühendislik]
order: 6.5
translation_url: /en/Cisco_Module4_2
---

#### 4.4.5 Lab – Using the Browser Exploitation Framework (BeEF)

##### Part 1 Load the BeEF GUI Environment

**Step 1: Start BeEF**

Application> All Application> beef start menüsünden aracımızı çalıştıralım. İlk çalıştırdığımızda bizden şifreyi değiştirmemizi isteyecektir. Şifreyi değiştirin ve unutmayın.

GUI açıldıktan sonra bilgilerimizle giriş yapıyoruz.

- Username: beef
- Password: şifreniz

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

Burada yer alan Module Tree tarayıcıya yönelik gerçekleştirebilecek tüm saldırı, bilgi toplama ve sosyal mühendislikleri kategorilere ayırmış şekilde gösterir.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/browser.webp' | relative_url }}" width="500" height="330" alt="BeEF Commands sekmesinde Module Tree kategorilerinin listesi">
</div>

Bu menü üzerindekileri genişletirsek her fonksiyonun yanındaki renk kodlarını fark edeceksiniz. Her renk kodunun farklı bir anlamı vardır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/renkkod.webp' | relative_url }}" width="200" height="600" alt="BeEF modüllerinin renk kodlarına göre listelenmiş görünümü">
</div>

- **Yeşil**: Bu komut modülü hedefe karşı çalışıyor ve kullanıcıya görünmezdir.
- **Turuncu**: Bu komut modülü hedefe karşı çalışıyor fakat kullanıcıya gözükebilir.
- **Beyaz**: Bu komut modülü hedefe karşı doğrulanmış değil.
- **Kırmızı:** Bu komut modülü kullanıcıya karşı kullanılamıyor.

**Not**: Module Tree aynı bir filtre gibi kullanılır ve burada arama yapabilirsiniz.

Network menüsüne gidelim. Burada kurban ile olan ağ topolojisini görebilirsiniz. Biz local üzerinde çalıştığımız için sadece bir ağ ve bir hostu gösterecektir. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule4/hooked.webp' | relative_url }}" width="400" height="240" alt="BeEF Network sekmesinde kurban ile ağ topolojisi görünümü">
</div>

**Step 2: Use BeEF to initiate a social engineering attack**

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

- Yeni bir Mozilla sayfası açın.
- Yeni bir sayfa üzerinden [http://127.0.0.1:3000/ui/authentication](http://127.0.0.1:3000/ui/authentication) açın.
- Sisteme bilgilerinizle giriş yapın.
- Mozilla üzerinden [http://127.0.0.1:3000/demos/butcher/index.html](http://127.0.0.1:3000/demos/butcher/index.html) adresine erişin.
- BeEF kontrol paneli üzerinden Online Browsers menüsünden Command sekmesini açın.
- Social Engineering kategorisinden TabNabbing seçin.

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

- **Authority**: Sosyal mühendislikte hem özgüven hem de belki otorite gösterir.
- **Scarcity and Urgency**: Aciliyet duygusunu arttırmak kurbanı manipüle etmek için kullanılan bir yöntemdir.
- **Social Proof**: İnsanlar bir durum karşısında nasıl davranacağını bilemediğinde, başkalarının davranışlarını örnek almasıdır.
- **Likeness**: İnsanların hoşlandıkları kişilerden daha kolay etkilendiği için güzel görünümlü hoş birini kullanmak daha çok işe yarar.
- **Fear**: İnsanlar başlarına kötü bir şey gelecek düşüncesiyle endişeyle düşüncesiz hareketler sergileyebilir.
