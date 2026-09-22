---
categories: [modul]
layout: post
description: "Cisco Ethical Hacker kursunun üçüncü bölümünün pasif bilgi toplama kısmının ikinci parçasıdır. DNS sorguları, WHOIS, SSL sertifika analizi ve şirket itibarı/güvenlik duruşu araştırma teknikleri uygulamalı olarak anlatılmıştır."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Modül 3 - Passive Recon (2/2)
tags: [Cisco, Pasif Keşif]
order: 3.5
translation_url: /en/Cisco_Module3_Passive2
---

#### 3.1.4 DNS Lookups

DNS sorguları yapılarak hedef sistemin IP adresini veya varsa kullanılan diğer alt alan adlarını öğrenmeye çalışılabilir.

dnsrecon ve dig toolları kullanılabilir.

#### 3.1.5 Identification of Technical and Administrative Contacts

Bir domain hakkında teknik ve idari iletişim bilgilerine bakmak için whois komutunu kullanabiliriz. Örnek olarak h4cker.org sitesine bakalım.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> whois h4cker.org
</div>

#### 3.1.6 Lab – DNS Lookups

##### Part 1 Use nslookup to Obtain Domain and IP Address Information

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

Verilen çıktıda skillsforall.com adresini Google’un DNS sunucu ile çözümlemeye çalışıyoruz. Google DNS sunucusunun IP adresi 8.8.8.8.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup skillsforall.com 8.8.8.8
</div>

İnteraktif modda server’ı değiştirmek için;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nslookup<br>> server 8.8.8.8<br>> set type=any<br>> skillsforall.com
</div>

Type olarak “any” seçtiğimiz zaman, etki alanları hakkında bütün bulabildiği bilgileri gösterir.

##### Part 2 Use Whois Function to Obtain Domain Information

Whois, DNS sunucu kayıtları yerine alan adı nerede ve kim, fiziksel adres ve teknik bilgilere erişim için kullanılan bir araçtır.

 **Step 1: Use whois to determine IP address registration information**

Nslookup cisco.com çıktısından aldığımız bilgi ile cisco.com’un name server’ı olan ns1.cisco.com adresinin IP bilgisini bulduk. IP adresi 72.163.5.201 idi. Bu IP adresini whois ile taratalım. Böylece IP adresinin scope aralığını bulalım.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/whois.webp' | relative_url }}" width="660" height="330" alt="whois sorgusuyla elde edilen IP adresi kayıt ve scope bilgileri">
</div>


##### Part 3 Compare the Output of the Nslookup and Dig Functions

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

##### Part 4 Perform Reverse DNS Lookups

Ters DNS ya da diğer ismiyle rDNS, bir IP adresini kullanarak o adrese karşılık gelen sunucu adlarını bulmaya çalışır.

**Step 1: Use Dig to perform rDNS lookups**

Daha önceden bulduğumuz ns1.cisco.com adresinin IP adresini deneyelim.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> dig -x 72.163.5.201
</div>

Aşağıdaki çıktıda görüldüğü üzere hostname bulduk.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/dig.webp' | relative_url }}" width="660" height="370" alt="dig -x komutuyla yapılan ters DNS sorgusunun hostname sonucu">
</div>


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

#### 3.1.7 Cryptographic Flaws

Sitelerin SSL sertifikaları incelenerek zayıf sertifikalar veya kriptografik zayıflıklar gibi çeşitli bilgilere erişilebilir.

Crt.sh gibi bir site üzerinden istediğiniz kurum veya sayfanın sertifikası sorgulanabilir. Örnek olarak h4cker.org adresini inceleyelim.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/lets.webp' | relative_url }}" width="630" height="210" alt="crt.sh üzerinde h4cker.org için sertifika şeffaflığı (CT) sorgu sonuçları">
</div>

Daha önceden bilmediğimiz subdomain adreslerini burada da görebiliriz.

#### 3.1.8 Lab – Finding Information from SSL Certificates

Bazı SSL sertifikaları, ağ üzerinde yerel olarak hostta saklanır. İstemci ve sunucu arasında güvenli iletişim kurulmasını sağlar. SSL sertifika doğrulma zinciri için host hem ara hem de kök SSL sertifikalarını tutar.

##### Part 1 Access Detailed Certificate Information Online

Certificate Transparency hem SSL hem de TLS sertifikalarının yayınlanmasını izlemek ve denetlemek için kullanılan açık bir çerçevedir.

Her yeni bir sertifika veya bir sertifika hareketi log altına alınır böylece ortaya CT log dediğimiz terim ortaya çıkar. Hem saldırganlar hem de koruyanlar bu CT loglarını kullanarak kendi amacına uygun bilgi elde edebilir.

##### Part 2 Use SSL Analysis Tools in Kali

Kali üzerindeki bazı SSL toollarının isimlerini ve amaçlarını anlatalım.

| Araç Adı | Açıklama / Kullanım Amacı |
|---|---|
| sslscan | Bir sunucunun desteklediği SSL/TLS protokollerini, şifreleme algoritmalarını (cipher) ve zayıf konfigürasyonlarını hızlıca listeler. Özellikle zayıf SSL versiyonlarını ve cipher'ları tespit etmek için kullanılır. |
| ssldump | Canlı SSL/TLS trafiğini analiz eder. Ağ üzerinden geçen şifrelenmiş trafiği çözümlemeye çalışır (özellikle SSLv2/3 gibi eski sürümler varsa işe yarar). Wireshark gibi çalışır ama özellikle SSL için özelleştirilmiştir. |
| sslh | Aynı port üzerinden (genellikle 443) gelen farklı protokolleri (SSH, HTTPS, OpenVPN vs.) ayırt ederek uygun arka uca yönlendirir. Port paylaşımı sağlar. Örn: hem SSH hem HTTPS 443 üzerinden çalışabilir. |
| sslyze | Güçlü bir SSL güvenlik analiz aracıdır. Bir sunucunun TLS yapılandırmasını detaylı şekilde test eder (cipher desteği, sertifika doğruluğu, Heartbleed, session resumption vs.). Otomasyon dostudur. |
| sslsplit | SSL/TLS trafiğini "ortada adam" (MITM) gibi araya girerek şifre çözme (decrypt) için kullanılır. Trafiği ikiye ayırır: istemciye sunucu gibi, sunucuya istemci gibi davranır. Genellikle pentest ve kırmızı takım faaliyetlerinde kullanılır. |


##### Part 3 Use Kali Tools to Gather Certificate Information

Sslscan, bilindiği üzere SSl sertifikaları hakkında bilgi verir. Bir başka kullanacağımız araç ise “aha” aracıdır. Outputu HTML dosyasına çevirmeye yarar.

**Step 1: Run sslscan and save the output to a HTML file**

Kali üzerinde hedefimiz için bir sslscan taraması yapıyoruz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sslscan skillsforall.com | aha > sfa_cert.html
</div>

Dosyanın konumunu bulduktan sonra Mozilla üzerinde html dosyasını açabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/html.webp' | relative_url }}" width="500" height="410" alt="sslscan çıktısının aha ile oluşturulan HTML raporunun tarayıcı görünümü">
</div>


#### 3.1.9 Company Reputation and Security Posture

Eğer şirketin daha önceden veri sızdırılma geçmişi varsa saldırganlar eski saldırıdan kalan

- Şifre dökümleri
- Dosya meta verileri
- Web sitesi arşivleme
- Public kaynak kod depoları

kullanabilirler.

##### Password Dumps

Saldırganların daha önceden çalınan şifre dökümlerine ulaşmak için birçok araçlara sahiptir. Bunlardan birisi h8mail aracıdır.

Kali üzerinde pip ile kurulum yapmak için ilk öncelikle izole ortamımızı oluşturalım.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> python3 -m venv cisco<br>source cisco/bin/activate<br>pip install h8mail
</div>

Böylelikle h8mail aracımızı kurabiliriz. Bu araca benzer olarak diğer araçlardan bazıları aşağıda linkleriyle birlikte verilmiştir.

*   **WhatBreach:** [_https://github.com/Ekultek/WhatBreach_](https://github.com/Ekultek/WhatBreach)
*   **LeakLooker:** [_https://github.com/woj-ciech/LeakLooker_](https://github.com/woj-ciech/LeakLooker)
*   **Buster:** [_https://github.com/sham00n/buster_](https://github.com/sham00n/buster)
*   **Scavenger:** [_https://github.com/rndinfosecguy/Scavenger_](https://github.com/rndinfosecguy/Scavenger)
*   **PwnDB:** [_https://github.com/davidtavarez/pwndb_](https://github.com/davidtavarez/pwndb)

##### File Metadata

Fotoğraf, Word, Excel ve benzeri dosyaların metadata bilgilerinden birçok bilgi öğrenebiliriz. Bu bilgileri görebileceğimiz birçok araç vardır. Bunlardan biri de ExifTool aracıdır.

##### Strategic Search Engine Analysis/Enumeration

Günümüzde piyasada birçok farklı arama motoru bulunmaktadır. Kullanıcılar tercihlerine göre Yandex, Bing veya DuckDuckGo gibi arama motorlarını kullanabilirler. Ancak Google, sahip olduğu gelişmiş arama operatörleri sayesinde çok daha detaylı ve hedefli aramalar yapmaya olanak tanır. Bu yöntem, özellikle siber güvenlik dünyasında Google Dorking olarak bilinir ve hassas bilgilere erişmek amacıyla kötü niyetli kişiler tarafından da kullanılabilir.

Bazı özel arama operatörlerinden örnek aşağıdadır.

- **Filetype:** Google üzerinde yalnızca belirli bir dosya türünde arama yapar.
- **Inurl:** Google üzerinde URL üzerinde olacak kelimeyi belirler.
- **Link**: Google üzerinde yalnızca belirli bir terimi içeren bağlantılarda tarama yapar.
- **Intitle:** Google üzerinde bir doküman başlığında belirli bir terimi aramasını sağlar.

Örnek bir arama aşağıda yer almaktadır.

"public $user =" | "public $password = " | "public $secret =" | "public $db =" ext:txt | ext:log -git

[https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database) sitesi üzerinde dork örneklerini bulup inceleyebilirsiniz.

##### Website Archiving/Caching

Bazı siteler internet üzerindeki sitelerin bilgilerini arşivleyip depolar. [https://web.archive.org/](https://web.archive.org/) adresi üzerinden baktığınız sitenin zamanda eski haline giderek siteyi görebilirsiniz.

##### Public Source Code Repositories

Saldırganlar, Github veya Gitlab üzerinde public olan kod kaynağına ulaşarak değerli bilgiler elde edebilir veya sistemin açığını bulabilir.

#### 3.1.10 Lab – Finding Out About the Organization

##### Part 1 Find Information about Email Breaches.

Çalışanların iş maili daha önceden ifşa edildiyse bu bilgi kullanılabilir. Bazı online servisler mailin ifşa edilip edilmediğini öğrenmek için kullanılabilir.

- haveibeenpwned.com
- f-secure.com
- hacknotice.com
- breachdirectory.com
- keepersecurity.com

**Step 1: Use a tool to find email adresses for a domain**

Örnek olarak Kali’de yüklü olarak gelen emailharvester toolunu kullanabiliriz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> emailharvester -d example.com
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_passive/searching.webp' | relative_url }}" width="400" height="380" alt="emailharvester aracının example.com için bulduğu e-posta adresleri">
</div>


**Step 2: Use Spiderfoot to research email adresses**

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> spiderfoot -l 127.0.0.1:5001
</div>


Komutu ile ara yüzümüzü çalıştırdıktan sonra erişim sağlayabiliriz. Burada new scan diyerek email için olan modüllerle arama yapabiliriz. Birkaç email modülünden örnek verecek olursam; Ahmia, AccountFinder, Archive.org, EmailCrawl.

Başka modül araştırarak da scanleyebilirsiniz.

##### Part 2 View File Metadata

File metadataları saldırganlar için birçok değerli bilgi içerebilir. Mesela fotoğrafın oluşturulduğu cihaz hakkında bilgi verebilir. Saldırgan da bu cihazın potansiyel zafiyetlerini araştırarak öğrenebilir veya bir başka örnek olarak dosyanın yapımcısının ismi, dosyanın ne zaman oluşturulduğu gibi bilgiler öğrenilebilir.

**Step 1: Use Exiftool**

Exiftoolun kurulumunu tamamladıktan sonra [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database) üzerinden çeşitli dorking aratıp gizli belgeleri indirdikten sonra exiftool ile dosyanın metadataları incelenebilir.

Tüm dosyayı taramak için ise -csv parametresi kullanılabilir.
