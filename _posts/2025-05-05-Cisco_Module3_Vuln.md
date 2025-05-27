---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun üçüncü bölümünün zafiyet taraması kısmıdır. Zafiyet tarayıcılarının çalışma prensipleri, tarama türleri (authenticated, unauthenticated, stealth, compliance vb.) ve Kali Linux üzerinde Nmap ile GVM araçları kullanılarak yapılan zafiyet analizleri uygulamalı olarak ele alınmıştır. Ayrıca, tarama sonuçlarının analizinde dikkat edilmesi gereken noktalar ile CVE, CWE, CVSS gibi güvenlik kaynakları tanıtılmıştır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Ethical Hacker Modül 3 - Vulnerability Scans
order: 5
---
# Cisco Ethical Hacker

# Module 3: Information Gathering and Vulnerability Scanning

## 3.3 Understanding the Art of Performing Vulnerabilitiy Scans

### 3.3.1 How a Typical Automated Vulnerability Scanner Works

![](./assets/images/Resim54.jpg)

Birbirinden farklı da olsa çoğu zafiyet tarayıcısı benzer bir süreci takip eder. Görselleştirilmiş hali yukarıda verilmiştir.

**Step 1: Keşif Aşaması**

Tarayıcı, nmap gibi bir araç kullanarak ağ üzerindeki host ve port taraması keşfi yapar.

**Step 2: Servis Tanımlama ve Kayıt**

Tarayıcı portu açık gördüğü zaman üzerinde daha fazla bilgi edinmeye çalışır. Hangi yazılımın ve sürümün kullanıldığını belirlemeye çalışır. Örneğin banner grabbing.

**Step 3: Zafiyet Karşılaştırılması**

Tarayıcı, bulduğu bu bilgiler ile kendi zafiyet verita-banı arasında bir kıyaslama yaparak, bilinen zafiyetlere karşı savunmasız olup olmadığını kontrol eder.

**Step 4: Rapor Oluşturma**

Tarayıcı, potansiyel zafiyetleri içeren bir rapor üretir.

### 3.3.2 Types of Vulnerability Scans

Test yapılacak ortama göre tarama yöntemleri ve türleri değişiklik gösterilebilmektedir.

#### Unauthenticated Scans

Tarayıcılar genel olarak kullanıcı bilgisi olmadan tarama yapar. Ağ üzerinde ifşa edilmiş servisleri veya açık olan portları tararlar. Eğer bağlantı güvenlik duvarı tarafından bloklanırsa portlar kapalı olarak gözükmektedir.

#### Authenticated Scans

Kimlik bilgilerini kullanarak tarama, tarayıcı root düzeyinde erişim sağlayan bir tarama türüdür. Tarayıcı, SSH veya farklı bir servis ile hedef sisteme gerçekten giriş yapar, sistemin içerisindeyken de netstat gibi komutları çalıştırarak bilgi öğrenmeye çalışır.

#### Discovery Scans

Keşif taraması saldırının yüzeyini belirlemek için kullanılır. Tarayıcı hem port hem de port üstünde olan servisleri daha detaylı arayarak bilgiler toplamaya çalışır. Örnek olarak port taraması sonucunda 80, 22 ve 443 numaralı portlar açıksa, 80 ve 443 üstünde hangi web sunucusunun çalıştığı hangi sürüm olduğunu tespit edip saldırı yüzeyini ayarlayabilir.

#### Full Scans

Bu zamana kadar anlatılan tarama türlerinin etkinleştirilmesi ile meydana gelir. Kullanılan işletim sistemi veya makineye göre değişim gösterebilmektedir.

Popüler bir tarama aracı olan Nessus üzerinde mesela çeşitli, işletim sistemi veya makine türüne göre pluginler yer almaktadır.

#### Stealth Scans

Hedefin farkına varmadan yapılan gizli olan tarama türüdür. Mesela daha önceden nmap tarama türlerinden hangisinin en sessiz olduğunu öğrenmiştik. Aynı bu gibi örnekler diğer zafiyet tarama araçlarından da geçerlidir. Onlar üzerinde de sessiz tarama yapma seçenekleri vardır.

#### Compliance Scans

Bu eğitimde daha öncesinde de gördüğümüz gibi şirketlerin uyması gereken bazı yönetişimler vardır. Şirketlerin ve şirket ürünlerinin bu kurallara uyup uymadığını test etmek üzere zafiyet tarayıcısı kullanılabilir.

Çoğu zafiyet tarayıcısı özel uyumluluk politikaları oluşturma yeteneğine sahiptir.

### 3.3.3 Lab – Vulnerability Scanning with Kali Tools

Daha önceki senaryomuzdaki gibi 10.6.6.23 IP adresli cihaz şüpheli davranışlar sergiliyor biz de onu inceliyoruz.

#### Part 1 Run a Nmap Scan on a Target Computer

**Step 1: Identify open ports and services**

Portları ve servislerin sürümlerini öğrenmek için bir nmap taraması gerçekleştiriyorum.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sV 10.6.6.23
</div>

![](./assets/images/Resim55.jpg)

İşletim sistemini bulmak için ise aşağıdaki komut;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo nmap -O 10.6.6.23
</div>

![](./assets/images/Resim56.jpg)

**Step 2: Use the nmap Vulners script tos can for vulnerabilities**

Vulners scripti açık port ve yazılım versiyon bilgisini tutarak CPE veritabanı ile kıyaslama yapar. Böylece sistemin, bilinen zafiyetlere karşı açıklığı olup olmadığını kontrol eder.

CVE skoru 4 veya daha yüksek olan sistemde olan zafiyetleri taramak için aşağıdaki komutu girelim.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sV –script vulners –script-args mincvss=4 10.6.6.23
</div>

![](./assets/images/Resim57.jpg)

Görüldüğü üzere sistemde birçok yüksek potansiyel zafiyet bulunmaktadır.

#### Part 2 Use GVM to Scan for Vulnerabilities

GVM, en yaygın kullanılan açık kaynaklı güvenlik tarayıcılarından biridir. Cisco Kali üzerinde GVM yüklü olsa bile doğrulamak için aşağıdaki komutu kullanabiliriz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo gvm-check-setup
</div>

Ara yüze erişmek için;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo gvm-start
</div>

Ara yüze eriştikten sonra tarama başlatmak için Scans > Tasks sayfasına gelin. Sol üst tarafta yer alan üç tane simgeden asaya benzeyeni seçin.

![](./assets/images/Resim58.jpg)

**Step 3: Scan the target host for vulnerabilities**

Yukarıdaki çıktıda da görüldüğü üzere IP adress yerine hedefimiz olan 10.6.6.23 veya gravemind.vm adresini yazabilirsiniz Yazdıktan sonra Start Scan butonuna tıklayın. Taramanın bitmesi biraz sürebilir.

![](./assets/images/Resim59.jpg)

Bizi böyle bir sayfa karşılıyor. Bu sayfada Date bilgisine tıklarsak bulunan CVE’ler veya host hakkında daha fazla bilgiye erişebiliriz. 

![](./assets/images/Resim60.jpg)

### 3.3.4 Challanges to Consider When Running a Vulnerability Scan

·        **Considering the best time to run a scan**: Lab ortamlarında değil de canlıya çıkan uygulamalar üzerinde testler yapmak çeşitli riskleri de yanında getirir.

·        **Determing what protocols are in use:** Tarama yapmaya başlamdan önce ilk yapılacaklar arasında hedef sistemin hangi protokolleri kullandığını belirlemek vardır.

·        **Network Topology:** Ağ tpolojisi saldırı planını yapmak için çok önemlidir. WAN gibi ağlar üzerinde test yapılması önerilmez. Hedefe en yakın konumda bulunarak tarama yapılması önerilir.

·        **Bandwith Limitations:** Tarama yapılan ağın bant genişliği göz önünde bulundurulmalıdır. Örneğin VPN ya da WAN gibi düşük bant genişliğine sahip ağlar üzerinden tarama yapıyorsanız tarama seçeneklerini bu duruma göre ayarlamalısınız.

·        **Query Throttling:** Bant genişliği sınırlı olan bir ağda tarayıcının trafiğini yavaşlatmaya denir. Örneğin Linux bir makinede Windows makine zafiyetlerini taramaya gerek yoktur.

·        **Fragile Systems:** Tarama yaparken oluşan trafiğe dayanamayan cihazlar vardır. Bu tür sistemleri tararken ya daha az trafik göndermeli ya da tarama kapsamından çıkartmalısınız.

## 3.4 Understanding How to Analyze Vulnerability Scan Results

### 3.4.1 Sources for Further Investigation of Vulnerabilities

·        **US-CERT**: Kamu ve özel kuruluşlar ile birlikte zafiyet bilgi paylaşım etkinliğini artırmak amaçlarındandır.

·        **The CERT Division of Carneige Mellon University**: Güvenlik açıkları üzerine araştırma yapar ve siber güvenlik alanındaki çalışmalara katkıda bulunur.

·        **NIST**: Organizasyonların siber güvenlik duruşlarını iyileştirmek için kullanılabilecek standartları ve endüstri en iyi uygulamalarını özetlemektedir.

·        **JPCERT**: Aynı US-CERT gibi fakat Japonya’nın siber güvenlik birliğidir.

·        **CAPEC**: Bilinen saldırıların sözlüğüdür.

·        **CVE**: Bir CVE Kimliği (ID), "CVE" harfleri ile başlayıp, yayım yılı ve kimlik numarasının sıralama kısmında dört veya daha fazla haneli bir sayı içerir (örneğin, CVE-YYYY-NNNN, dört haneli bir sıralama numarasıyla; CVE-YYYY-NNNNN, beş haneli sıralama numarasıyla; CVE-YYYY-NNNNNNN, yedi haneli sıralama numarasıyla vb.).

·        **CWE**: Zafiyetlerin temel nedenleri olan yazılım güvenliği zayıflıklarını tanımlamak için ortak bir dil oluşturmak

**CVSS**: Bir zafiyetin ciddiyetini hesaplamak için en yaygın kullanılan standartlardan biri, Ortak Zafiyet Skorlama Sistemi (CVSS)'dir.


