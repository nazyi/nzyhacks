---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun ikinci bölümüdür. Sızma testi sürecinde planlama ve kapsam belirleme aşamalarının neden kritik olduğunu vurgular. Aynı zamanda regülasyonlara uyum, yasal sorumluluklar ve etik ilkeler çerçevesinde nasıl hareket edilmesi gerektiğini detaylandırır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Modül 3 
---

# Cisco Ethical Hacker

## Module 3: Information Gathering and Vulnerability Scanning

## 3.1 Perform Passive Reconnaissance

### 3.1.1 Reconnaissance  

Hedef hakkında bilgi toplamaya reconnaisance denir. Cyber KillChain’nin ilk adımıdır. Askeri anlamında keşif anlamında kullanılan bu terim, düşmanın konumu ve yetenekleri gibi bilgileri kapsamaktadır.

### 3.1.2 Active Reconnaissance vs Passive Reconnaissance

**Active Reconnaissance**, bilgi toplamak için kullanılan toollar daha saldırgan ve belirgin olmasıdır. Hedef sisteme veya ağa istek atarak çeşitli taramalar yapar.

**Passive Reconnaissance**, kullanılan toolların hedef sistem veya ağ ile doğrudan etkileşime girmediği durumdur. Hedefe kendini fark ettirmeden pasif bir yol izleyerek bilgi toplanmaya çalışılır.

Bazı aktif bilgi toplama tooları:

·        Host Enumeration

·        Network Enumeration

·        User or Group Enumeration

·        Application, Service, Packet Enumeration

Bazı pasif bilgi toplama toolları:

·        OSINT

·        Recon-ng

·        Domain Enumeration
### 3.1.3 Lab – Using OSINT Tools

#### Part 1 Examine OSINT Resources

 [https://osintframework.com/](https://osintframework.com/) OSINT Frameworkünü kullanarak nickname aratabiliriz.  [https://whatsmyname.app/](https://whatsmyname.app/) sitesi ile istediğiniz nickname’i arayabilir. Çıkan sonuçların urlsi ile birlikte bulabilirsiniz.

#### Part 2 Use SpiderFoot

Kali’de spiderfootu açtıktan sonra toolu kullanmak için

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> spiderfoot -l 127.0.0.1:5001
</div>

Bu komutu yazdıktan sonra tarayıcı üzerinden ip adresini ve portu açıp SpiderFoot ara yüzüne erişebilirsiniz.

![](./assets/images/Resim3.jpg)

**Step 1: Run SpiderFoot scan for a Domain**

Ara yüz üzerinde New Scan diyerek yeni bir scan yapalım. Scan Name kısmına scan adımızı, Scan Target kısmına hedef domainimizi yazıyoruz. Aşağıda yer alan “By Use Case”, “By Reired Data” ve “By Module” kısımlarından gerekli ayarlamaları yapabilirsiniz. Biz şimdilik test için h4cker.org sitesini Footprint case’ini kullanarak deniyoruz.

**Step 2: Investigate Scan Results**

Scan tab’ine bakarak önceki scanler veya aktif olarak devam eden scanlere bakabiliriz. Cisco1 isimli test scanimizin üstüne tıklayarak şu ana kadar çeşitli modüller tarafından elde edilen bilgilere bakabilirsiniz. 

**Step 3: Register for API Keys**

Bazı modülleri kullanmak için API anahtarlarına ihtiyaç vardır. Bu API anahtarları bazı modülleri için ücretsiz alınabilmektedir. Kullanmak istediğiniz modülün sayfa içeriğine giderek soru işaretine tıklayarak API anahtarının nasıl alınacağı adım adım görebilirsiniz.

#### Part 3 Investigate Recon-ng

**Step 1: Create a Workspace**

Kali üzerinde recon-ng toolumuzu açıyoruz. Bunu gerek terminal üzerinden gerek Kali menüsü üzerinden aratarak bulabilirsiniz.

Yapılan her sorgunun kendine ayrı çalışma alanı vardır. Böylece sorgular birbirine karışmaz iş kolaylaşır.

Workspace oluşturmak için “workspaces create”” komutunu kullanıyoruz.

**Step 2: Investigate Modules**

Recon-ng toollu modüler bir çerçevedir. Yani bir sürü modülden oluşmaktadır. Bu modülleri dışarı bir marketpace üzerinden indirip kullanabilirsiniz. “modules search” komutunu kullanarak modüllere bakabiliriz.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][default]</span> > marketplace search
</div>

**Step 3: Investigate the Module Marketplace**

Modüllere Github reposundan ulaşılabilir. Modüller hakkında detaylı bilgiye ulaşmak için ise marketplace info <module\_name> kullanarak ulaşılabilir.

**Step 4: Install a new module**

Yeni modül indirmek için ilk öncelikle modüle search ile modülleri görüntüleyelim.

![](./assets/images/Resim6.jpg)

Biz örnek olarak bing\_domain\_web modülünü indirelim. İndirmek için;

<div class="code-window">
<br>
<span class="highlight">[recon-ng][default]</span> > marketplace install recon/domain-hosts/bing_domain_web
</div>

Aynı işlemi hackertarget modülü için de uygulayıp modülü indirin.

**Step 5: Run the New Modules**

Yeni bir workspace oluşturalım.  Modül ile çalışmak için aşağıdaki komutunu kullanalım.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco]</span> > modules load hackertarget 
</div>

Modül hakkında daha fazla bilgi almak istersniz aşağıdaki komutu kullanabilirsiniz.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > info 
</div>

Info çıktısındaki gibi biz gereken tek ayar source yani kaynağın ayarlanmasıymış.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > options set source hackxor.net<br>SOURCE -> hackxor.net
</div>


Komutu ile hedefimizi ayarlayalım. Tekrardan info diyerek ayarlanıp ayarlanmadığına bakabiliriz.
“run” komutu ile modülümüzü çalıştıralım.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > run
</div>

![](./assets/images/Resim7.jpg)

Toplanan bilgilerin genel bir özetini tablo halinde görmek istiyorsak “dashboard” komutunu kullanabiliriz. 

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > dashboard
</div>

![](./assets/images/Resim8.jpg)

Dashboard üzerinden aldığımız görüntüdeki başlıklara bakmak için ise “Show” komutunu kullanabiliriz. Örnek kullanım “show hosts”.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][hackertarget]</span> > show hosts
</div>

![](./assets/images/Resim9.jpg)

**Step 6: Investigate the Web Interface**

Recon-ng’nin veritabanındaki sonuçları daha iyi görüntüleyebilmek için web ara yüzü vardır.

Yeni bir terminal açıp recon-web yazalım. Böylece databasedeki bilgilerin toplanma süreci başlar. Outputta çıkan URL üzerine tıklayarak ara yüze erişebilirsiniz. Ara yüzde ilk başta default workspace’in sonuçları gelir yukarıdaki turuncu yazan default yazısına tıklayarak kendi workspace’inizi seçebilirsiniz.

![](./assets/images/Resim10.jpg)

#### Part 4 Find Interesting Files with Recon-ng

Site üzerinde değişik dosyalar bulmak için yeni bir modül indirelim.

![](./assets/images/Resim12.jpg)

Modülü indirmek ve kullanmak için;

<div class="code-window">
<br>
<span class="highlight">[recon-ng][default]</span> > marketplace install discovery/info/disclosure/interesting_files<br><span class="highlight">[recon-ng][default]</span> >	modules load interesting_files<br><span class="highlight">[recon-ng][cisco][interesting_files]</span> > info
</div>

![](./assets/images/Resim13.jpg)

Gerekli ayarlara baktıktan sonra source yine hackxor.net olarak ayarlayalım.

<div class="code-window">
<br>
<span class="highlight">[recon-ng][cisco][intersting_files]</span> > options set source hackxor.net<br><span class="highlight">[recon-ng][cisco][intersting_files]</span> > run
</div>

![](./assets/images/Resim14.jpg)

Kaydedilen çıktıları /root/.recon-ng/workspaces/cisco/http\_hackxor.net\_robots.txt dosyasından okuyabilirsiniz.

recon-ng/data klasöürü içindeki csv dosyasının içinde de sonuçları okuyabilirsiniz.

### 3.1.4 DNS Lookups

DNS sorguları yapılarak hedef sistemin IP adresini veya varsa kullanılan diğer alt alan adlarını öğrenmeye çalışılabilir.

dnsrecon ve dig toolları kullanılabilir.

### 3.1.5 Identification of Technical and Administrative Contacts

Bir domain hakkında teknik ve idari iletişim bilgilerine bakmak için whois komutunu kullanabiliriz. Örnek olarak h4cker.org sitesine bakalım.
