---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun dördüncü bölümüdür. Zafiyet tarayıcılarının çalışma prensipleri, tarama türleri (authenticated, unauthenticated, stealth, compliance vb.) ve Kali Linux üzerinde Nmap ile GVM araçları kullanılarak yapılan zafiyet analizleri uygulamalı olarak ele alınmıştır. Ayrıca, tarama sonuçlarının analizinde dikkat edilmesi gereken noktalar ile CVE, CWE, CVSS gibi güvenlik kaynakları tanıtılmıştır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Modül 4
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

![](./assets/images/Resim61.jpg)

**Step 2**

Menü üzerinden Social-Engineering Attack seçeneğini seçelim.

![](./assets/images/Resim62.jpg)

**Step 3**

Çıkan menü üzerinden de Spear-Phishing Attack Vectors seçeneğini seçelim.

![](./assets/images/Resim63.jpg)

**Step 4**

Burada bize yine birkaç tane seçenek sunuluyor biz 2. Seçeneği seçiyoruz.

![](./assets/images/Resim64.jpg)

**Step 5**

Burada file formatı seçmemiz isteniliyor. Biz 13. Seçenekten devam ediyoruz.

![](./assets/images/Resim65.jpg)

**Step 6**

E-maile koyacağımız PDF dosyasının formatının nasıl olduğunu seçiyoruz. Boş pdf seçeneği olan 2.yi seçiyoruz.

![](./assets/images/Resim66.jpg)

**Step 7**

Hangi tür reverse Shell kullanacağımızı seçiyoruz. Biz ilk seçeneği seçiyoruz.

![](./assets/images/Resim67.jpg)

**Step 8 – 9**

Shellin dinleme yapacağı IP adresi ve portu da verdikten sonra dosyanın adını değiştirmeyi veya değiştirmemeyi soruyor.

![](./assets/images/Resim68.jpg)

**Step 10**

Bu zararlıyı bir e-mail grubuna mı yoksa tek bir e-mail adresine mi gönderileceğini belirliyoruz. Tek bir adresi seçiyoruz.

![](./assets/images/Resim69.jpg)

**Step 11 – 14**

E-mailin içeriğini oluşturduktan sonra mail gönderime hazır.

### 4.4.2 Browser Exploitation Framework (BeEF)

XSS saldırısını kullanarak kullanıcı farklı kötü bir siteye yönlendirilerek çerezlerini çalmaya çalışır.

Browser Exploitation Framework ile XSS açıklarını kullanarak çerez çalmaya çalışılır.

Çalınan cookielerin örnek görüntüsü aşağıdadır.

![](./assets/images/Resim70.jpg)

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

![](./assets/images/Resim71.jpg)

Bu menüden sonra ise 2. seçenek olan “Website Attack Vectors” seçiyoruz.

![](./assets/images/Resim72.jpg)

Buradaki atakların açıklamasını okuduktan sonra bizim yapacağımız atak için 3. Seçenek olan “Credential Harvester Attack Method” seçiyoruz. 

![](./assets/images/Resim73.jpg)

**Step 2: Clone the DVWA.vm login screen**

Bu adımda DVWA.vm oturum açma web sitesini kopyalacağız. SET bilgisayarda barındılan bir web sitesi oluşturur. Kurbanlar buraya bilgilerini girerse istismar edilecek.

Aşağıdaki menüden Site Cloner seçeneğini seçiyoruz.

![](./assets/images/Resim74.jpg)

Bize web saldırganının IP adresini soruyor Kali makinemizde 10.6.6.0/24 bloğunda olduğumuz için 10.6.6.1 adresini giriyoruz. 

![](./assets/images/Resim75.jpg)

Şimdi ise klonlamak istediğimiz web sitesinin URL adresini giriyoruz. 

![](./assets/images/Resim76.jpg)

Başarılı bir şekilde dinlemeye başladık.

![](./assets/images/Resim77.jpg)

