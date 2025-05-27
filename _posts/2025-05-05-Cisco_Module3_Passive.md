---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun üçüncü bölümünün pasif bilgi toplama kısmıdır. Hedef sistemlerle doğrudan etkileşime girmeden bilgi toplama yöntemi olan pasif keşif (passive reconnaissance) anlatılmıştır. OSINT araçları, DNS sorguları ve WHOIS gibi tekniklerle, sistemler hakkında iz bırakmadan bilgi edinme yöntemleri uygulanmıştır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Ethical Hacker Modül 3 - Passive Recon 
order: 3
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
<span class="highlight">[recon-ng][cisco][interesting_files]</span> > options set source hackxor.net<br><span class="highlight">[recon-ng][cisco][interesting_files]</span> > run
</div>

![](./assets/images/Resim14.jpg)

Kaydedilen çıktıları /root/.recon-ng/workspaces/cisco/http\_hackxor.net\_robots.txt dosyasından okuyabilirsiniz.

recon-ng/data klasöürü içindeki csv dosyasının içinde de sonuçları okuyabilirsiniz.

### 3.1.4 DNS Lookups

DNS sorguları yapılarak hedef sistemin IP adresini veya varsa kullanılan diğer alt alan adlarını öğrenmeye çalışılabilir.

dnsrecon ve dig toolları kullanılabilir.

### 3.1.5 Identification of Technical and Administrative Contacts

Bir domain hakkında teknik ve idari iletişim bilgilerine bakmak için whois komutunu kullanabiliriz. Örnek olarak h4cker.org sitesine bakalım.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> whois h4cker.org
</div>

![](./assets/images/Resim15.jpg)

### 3.1.6 Lab – DNS Lookups

#### Part 1 Use nslookup to Obtain Domain and IP Adress Information

Nslookup hem Linux hem de Windows makinelerinde, temel olarak domain ismi ve IP adres bilgilerini getirir.

**Step 1: Using the nslookup command**

Sadece nslookup yazarsak interaktif moda geçebiliriz. Moda geçtikten sonra örnek olarak cisco.com domain adresine bakalım.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup<br>>cisco.com
</div>

Buradaki çıktıda hem IPv4 hem de IPv6 adreslerini görebilirsiniz. 
Domain adresinin name server bilgilerini görmek içinse;
<div class="code-window">
<br>
> set type=ns<br>> cisco.com
</div>

**Step 2: Change the server used to perform lookups**

Bazen DNS sunucusunun bir adresi çözümleyememesi veya cevap bulunamamasına çözüm olarak farklı bir DNS sunucu kullanabiliriz.

![](./assets/images/Resim16.jpg)

Yukarıda verilen çıktıda skillsforall.com adresini Google’un DNS sunucu ile çözümlemeye çalışıyoruz. Google DNS sunucusunun IP adresi 8.8.8.8.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup skillsforall.com 8.8.8.8
</div>

İnteraktif modda server’ı değiştimek için;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup<br>> server 8.8.8.8<br>> set type=any<br>> skillsforall.com
</div>

Type olarak “any” seçtiğimiz zaman, etki alanları hakkında bütün bulabildiği bilgileri gösterir.

#### Part 2 Use Whois Function to Obtain Domain Information

Whois, DNS sunucu kayıtları yerine alan adı nerede ve kim, fiziksel adres ve teknik bilgilere erişim için kullanılan bir araçtır.

 **Step 1: Use whois to determine IP address registration information**

Nslookup cisco.com çıktısından aldığımız bilgi ile cisco.com’un name server’ı olan ns1.cisco.com adresinin IP bilgisini bulduk. IP adresi 72.163.5.201 idi. Bu IP adresini whois ile taratalım. Böylece IP adresinin scope aralığını bulalım.

![](./assets/images/Resim17.jpg)

#### Part 3 Compare te Output of the Nslookup and Dig Functions

Dig, Nslookup’a benzeyen bir araçtır. Hedefin hostname’ini ve IP adresini çözümler.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com
</div>

IPv6 IP adresini görmek için ise;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com AAAA
</div>

Dig kullanarak ekstra bilgi edinmek için;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com 8.8.8.8 ns
</div>

Veya aynı nslookup’ta kullandığımız set type=any komutunu dig ile kullanımı;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig cisco.com any
</div>

#### Part 4 Perform Reverse DNS Lookups

Ters DNS ya da diğer ismiyle rDNS, bir IP adresini kullanarak o adrese karşılık gelen sunucu adlarını bulmaya çalışır.

**Step 1: Use Dig to perform rDNS lookups**

Daha önceden bulduğumuz ns1.cisco.com adresinin IP adresini deneyelim.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig -x 72.163.5.201
</div>

Aşağıdaki çıktıda görüldüğü üzere hostname bulduk.

![](./assets/images/Resim18.jpg)

**Step 2: Use the host utility to perform rDNS lookups**

Farklı bir IP adresinde “host” komutunu deneyelim.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> host 72.163.10.1
</div>

**Step 3: Use nslookup to perform rDNS lookups**

Daha önceden de kullandığımız şekilde nslookup kullanabiliriz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup 72.163.10.1
</div>

### 3.1.7 Cryptographic Flaws

Sitelerin SSL sertifikaları incelenerek zayıf sertifikalar veya kriptografik zayıflıklar gibi çeşitli bilgilere erişilebilir.

Crt.sh gibi bir site üzerinden istediğiniz kurum veya sayfanın sertifikası sorgulanabilir. Örnek olarak h4cker.org adresini inceleyelim.

![](./assets/images/Resim19.jpg)

Daha önceden bilmediğimiz subdomain adreslerini burada da görebiliriz.

### 3.1.8 Lab – Finding Information from SSL Certificates

Bazı SSL sertifikaları, ağ üzerinde yerel olarak hostta saklanır. İstemci ve sunucu arasında güvenli iletişim kurulmasını sağlar. SSL sertifika doğrulma zinciri için host hem ara hem de kök SSL sertifikalarını tutar.

#### Part 1 Access Detailed Certificate Information Online

Certificate Transparency hem SSL hem de TLS sertifikalarının yayınlanmasını izlemek ve denetlemek için kullanılan açık bir çerçevedir.

Her yeni bir sertifika veya bir sertifika hareketi log altına alınır böylece ortaya CT log dediğimiz terim ortaya çıkar. Hem saldırganlar hem de koruyanlar bu CT loglarını kullanarak kendi amacına uygun bilgi elde edebilir.

#### Part 2 Use SSL Analysis Tools in Kali

Kali üzerindeki bazı SSL toollarının isimlerini ve amaçlarını anlatalım.

![](./assets/images/Resim20.jpg)

#### Part 3 Use Kali Tools to Gather Certificate Information

Sslscan, bilindiği üzere SSl sertifikaları hakkında bilgi verir. Bir başka kullanacağımız araç ise “aha” aracıdır. Outputu HTML dosyasına çevirmeye yarar.

**Step 1: Run sslscan and save the output to a HTML file**

Kali üzerinde hedefimiz için bir sslscan taraması yapıyoruz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sslscan skillsforall.com | aha > sfa_cert.html
</div>

Dosyanın konumunu bulduktan sonra Mozilla üzerinde html dosyasını açabilirsiniz.

![](./assets/images/Resim21.jpg)

### 3.1.9 Company Reputation and Security Posture

Eğer şirketin daha önceden veri sızdırılma geçmişi varsa saldırganlar eski saldırıdan kalan

·        Şifre dökümleri

·        Dosya meta verileri

·        Web sitesi arşivleme

·        Public kaynak kod depoları

kullanabilirler.

#### Password Dumps

Saldırganların daha önceden çalınan şifre dökümlerine ulaşmak için birçok araçlara sahiptir. Bunlardan birisi h8mail aracıdır.

Kali üzerinde pip ile kurulum yapmak için ilk öncelikle izole ortamımızı oluşturalım.

·        python3 -m venv cisco

·        source cisco/bin/activate

·        pip install h8mail

Böylelikle h8mail aracımızı kurabiliriz. Bu araca benzer olarak diğer araçlardan bazıları aşağıda linkleriyle birlikte verilmiştir.

*   **WhatBreach:** [_https://github.com/Ekultek/WhatBreach_](https://github.com/Ekultek/WhatBreach)
*   **LeakLooker:** [_https://github.com/woj-ciech/LeakLooker_](https://github.com/woj-ciech/LeakLooker)
*   **Buster:** [_https://github.com/sham00n/buster_](https://github.com/sham00n/buster)
*   **Scavenger:** [_https://github.com/rndinfosecguy/Scavenger_](https://github.com/rndinfosecguy/Scavenger)
*   **PwnDB:** [_https://github.com/davidtavarez/pwndb_](https://github.com/davidtavarez/pwndb)

#### File Metadata

Fotoğraf, Word, Excel ve benzeri dosyaların metadata bilgilerinden birçok bilgi öğrenebiliriz. Bu bilgileri görebileceğimiz birçok araç vardır. Bunlardan biri de ExifTool aracıdır.

#### Strategic Search Engine Analysis/Enumeration

Günümüzde piyasada birçok farklı arama motoru bulunmaktadır. Kullanıcılar tercihlerine göre Yandex, Bing veya DuckDuckGo gibi arama motorlarını kullanabilirler. Ancak Google, sahip olduğu gelişmiş arama operatörleri sayesinde çok daha detaylı ve hedefli aramalar yapmaya olanak tanır. Bu yöntem, özellikle siber güvenlik dünyasında Google Dorking olarak bilinir ve hassas bilgilere erişmek amacıyla kötü niyetli kişiler tarafından da kullanılabilir.

Bazı özel arama operatörlerinden örnek aşağıdadır.

·        **Filetype:** Google üzerinde yalnızca belirli bir dosya türünde arama yapar.

·        **Inurl:** Google üzerinde URL üzerinde olacak kelimeyi belirler.

·        **Link**: Google üzerinde yalnızca belirli bir terimi içeren bağlantılarda tarama yapar.

·        **Intitle:** Google üzerinde bir doküman başlığında belirli bir terimi aramasını sağlar.

Örnek bir arama aşağıda yer almaktadır.

"public $user =" | "public $password = " | "public $secret =" | "public $db =" ext:txt | ext:log -git

[https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database) sitesi üzerinde dork örneklerini bulup inceleyebilirsiniz.

#### Website Archiving/Caching

Bazı siteler internet üzerindeki sitelerin bilgilerini arşivleyip depolar. [https://web.archive.org/](https://web.archive.org/) adresi üzerinden baktığınız sitenin zamanda eski haline giderek siteyi görebilirsiniz.

#### Public Source Code Repositories

Saldırganlar, Github veya Gitlab üzerinde public olan kod kaynağına ulaşarak değerli bilgiler elde edebilir veya sistemin açığını bulabilir.

### 3.1.10 Lab – Finding Out About the Orginization

#### Part 1 Find Information about Email Breaches.

Çalışanların iş maili daha önceden ifşa edildiyse bu bilgi kullanılabilir. Bazı online servisler mailin ifşa edilip edilmediğini öğrenmek için kullanılabilir.

·        haveibeenpwned.com

·        f-secure.com

·        hacknotice.com

·        breachdirectory.com

·        keepersecurity.com

**Step 1: Use a tool to find email adresses for a domain**

Örnek olarak Kali’de yüklü olarak gelen emailharvester toolunu kullanabiliriz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> emailharvester -d example.com
</div>

![](./assets/images/Resim22.jpg)

**Step 2: Use Spiderfoot to research email adresses**

spiderfoot -l 127.0.0.1:5001

Komutu ile ara yüzümüzü çalıştırdıktan sonra erişim sağlayabiliriz. Burada new scan diyerek email için olan modüllerle arama yapabiliriz. Birkaç email modülünden örnek verecek olursam; Ahmia, AccountFinder, Archive.org, EmailCrawl.

Başka modül araştırarak da scanleyebilirsiniz.

#### Part 2 View File Metadata

File metadataları saldırganlar için birçok değerli bilgi içerebilir. Mesela fotoğrafın oluşturulduğu cihaz hakkında bilgi verebilir. Saldırgan da bu cihazın potansiyel zafiyetlerini araştırarak öğrenebilir veya bir başka örnek olarak dosyanın yapımcısının ismi, dosyanın ne zaman oluşturulduğu gibi bilgiler öğrenilebilir.

**Step 1: Use Exiftool**

Exiftoolun kurulumunu tamamladıktan sonra [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database) üzerinden çeşitli dorking aratıp gizli belgeleri indirdikten sonra exiftool ile dosyanın metadataları incelenebilir.

Tüm dosyayı taramak için ise -csv parametresi kullanılabilir.
