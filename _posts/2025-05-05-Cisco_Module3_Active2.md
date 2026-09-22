---
categories: [modul]
layout: post
description: "Cisco Ethical Hacker kursunun üçüncü bölümünün aktif bilgi toplama kısmının ikinci parçasıdır. Paket inceleme, Scapy ile paket oluşturma ve Wireshark ile ağ trafiği analizi lab'ları uygulamalı olarak anlatılmıştır."
logo: "/assets/images/cisco.png"
author: nazy
title: Cisco Ethical Hacker Modül 3 - Active Recon (2/2)
tags: [Cisco, Aktif Keşif]
order: 4.5
translation_url: /en/Cisco_Module3_Active2
---

#### 3.2.4 Packet Inspection and Eavesdropping

Wireshark, tshark ve tcpdump gibi araçlarla paket yakalamaları yapılabilir, paketler incelenebilir ve dinleyebilirsiniz. Penetrasyon test uzmanları için bu tür araçlar, pasif keşif yapmak için kullanışlı olabilir. Tabii ki, bu tür bir keşif, hedefe fiziksel ya da kablosuz bir bağlantı gerektirir.

#### 3.2.5 Lab – Packet Crafting with Scapy

##### Part 1 Investigate the Scapy Tool

IP paketi göndermeden önce IP paketinin içeriğini anlamak önemlidir. Her IP paketinde, paket yapısı hakkında bilgi veren başlık eşlik eder. Her binary değeri IP paketinde farklı anlamlara gelmektedir.

ls() fonksiyonu ile alanlar hakkında detayları inceleyebilirsiniz. Scapy içerisinde fonksiyon kullanmanın genel mantığı function\_name (arguments) şeklindedir. Alanlar hakkında daha fazla bilgi almak için ise ls(IP) komutunu çalıştırabilirsiniz.

Aşağıdaki tabloda alan adları ve açıklamaları verilmiştir. 

| Alan Adı | Açıklama |
|---|---|
| Version | IP protokolünün versiyonunu belirtir (IPv4 için 4'tür). |
| Header Length | Başlığın uzunluğunu belirtir. |
| Type of Service (ToS) | Hizmet türünü belirtir; öncelik gibi bilgiler içerir. |
| Total Length | Tüm paketin (başlık + veri) toplam uzunluğu. |
| Identification | Paketi tanımlamak için kullanılır; fragmentasyon için önemlidir. |
| Flags | Paket bölme (fragment) işlemiyle ilgili kontrol bilgileri. |
| Fragment Offset | Parçalanmış paketlerin hangi sırada olduğunu belirtir. |
| Time to Live (TTL) | Paketin ağda ne kadar süre dolaşabileceğini belirler. |
| Protocol | Taşıdığı üst katman protokolünü belirtir (örneğin TCP: 6, UDP: 17). |
| Header Checksum | Başlığın doğruluğunu kontrol etmek için kullanılır. |
| Source IP Address | Paketi gönderen cihazın IP adresi. |
| Destination IP Address | Paketin hedef cihazının IP adresi. |
| Options (Opsiyonel) | Bazı özel durumlar için opsiyonel alanlardır. |
| Data (Veri) | IP paketinin taşıdığı esas veridir. |

##### Part 2 Use Scapy to Sniff Network Traffic

Ağ trafiğini, tcpdump veya tshark gibi görüntülemek için Scapy aracını kullanabiliriz.

**Step 1: Use the sniff() function**

Default olarak eth0 ağını dinlemek için direkt olarak;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff()
</div>

Sniff ile ağımızı dinliyorken yan terminal üzerinden pingleyerek gönderilen paket sayısını görüntüleyelim.

Scapy komut terminalinde dinlemeyi açtık. Yanda başka bir terminal üzerinde ping komutumuzu gönderelim.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ping -c 5 www.cisco.com
</div>

Scapy terminalinde Ctrl + C yaptıktan sonra gelen çıktıda gelen paketlerin sayısı yer almaktadır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed.webp' | relative_url }}" width="600" height="80" alt="Scapy sniff() sonrası yakalanan ping paketlerinin sayısını gösteren çıktı">
</div>

**Step 2: Capture and save traffic on a specific interface**

ifconfig üzerinde 10.6.6.1 ip adresinin interface ismini bir kenara not alalım. Scapy aracının terminale gelip aşağıdaki komutu yazalım;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”)
</div>

Yukarıda yaptığımız gibi sniff fonksiyonu ağı dinlemeye yaramaktadır. Fakat default olarak eth0 interface’ini dinlediğinden bahsetmiştik. Bu sefer bu komutta belirli bir interface üzerinden dinleme yapıyoruz. Br-internal ise virtual makineler için köprü interface idir.

Komutu girdikten sonra bu sefer Mozilla üzerinden 10.6.6.23 adresini açıyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/gravemind.webp' | relative_url }}" width="650" height="330" alt="Tarayıcıda 10.6.6.23 adresinde açılan Gravemind web sayfası">
</div>

Gravemind sayfası geldikten sonra Scapy terminalinden dinlemeyi durdurabiliriz Ctrl + C yaparak çıktıyı görüntüleyebilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed2.webp' | relative_url }}" width="600" height="80" alt="br-internal arayüzünde yakalanan trafiğin Scapy çıktısı">
</div>

Trafiği görüntülemek için ilk öncelikle bir değişkene kaydedip sonrasında görüntüleyebiliriz.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.summary()
</div>

**Step 3: Examine the collected packets**

Scapy üzerinden yine br-internal isimli interface’imizi dinlemeye alalım. Fakat bu sefer sadece ICMP protokolünün paketlerini ve toplamda 10 paket yakalamasını isteyelim.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”,filter=”ICMP”,count=10)
</div>

Farklı bir sekmeye giderek 10.6.6.23 IP adresine ping atalım.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ping -c 10 10.6.6.23
</div>

Scapy terminaline gelerek kaç tane ICMP paketinin yakalandığını görebilirsiniz. Örnek yukarıdaki çıktıda verilmiştir. Yakalanan paketleri kaydedip görüntülemek için;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.nsummary()
</div>

\*nsummary() ve summary() benzer fakat farklı komutlardır. nsummary() komutu birden fazla paketi görüntülemeye yararken summary() komutu yalnızca tek paketi görüntülemeye yarar.

Eğer paket hakkında daha fazla bilgi istersiniz paket numaralarının başındaki sıfırları almadan paketin numarasını yazarak bilgi alabilirsiniz. Aşağıda örneği verilmiştir;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a\[2\]
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/ether.webp' | relative_url }}" width="900" height="80" alt="Scapy'de a[2] komutuyla görüntülenen paket detay bilgisi">
</div>

Bu çıktıları pcap dosyası olarak kaydedip Wireshark üzerinde de inceleyebiliriz. Bunu yapmak için aşağıdaki komutları kullanabiliriz.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> wrpcap(“capture1.pcap”, a)
</div> 

Kaydedilen pcap dosyasını Wireshark üzerinde inceleyebiliriz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/pcap.webp' | relative_url }}" width="650" height="220" alt="wrpcap ile kaydedilen capture1.pcap dosyasının Wireshark görünümü">
</div>

##### Part 3 Create and Send an ICMP Packet

ICMP, ağ cihazları arasında kontrol mesajları göndermek amacıyla tasarlanmış bir protokoldür. Birçok farklı türde ICMP paketi vardır.

**Step 1: Use interactive mode to create and send a custom ICMP packet.**

Scapy terminali üzerinde “br-internal” isimli interface’i dinlemeye başlayalım.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”)
</div>

Dinlemeye başladıktan sonra yeni bir terminal açıp sudo izniyle birlikte tekrardan bir Scapy terminali açalım. Burada kendi ICMP paketimizi oluşturup 10.6.6.23 IP adresine göndereceğiz.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> send(IP(dst="10.6.6.23")/ICMP()/"This is a test")
</div>

Bu komutumuzu bölümleriyle birlikte inceleyelim.

- **IP(dst="10.6.6.23")**: Bu kısım IP katmanını oluşturur. dst ile paketin nereye gideceğini belirtiyoruz.
- **/ICMP()**: IP katmanının üstüne ICMP katmanı eklenir. Default olarak echo-request mesajı oluşturulur, eğer farklı bir tipte ICMP mesajı oluşturmak istiyorsanız type fonksiyonunu kullanabilirsiniz örneğin type=0.
- **/"This is a test"**: Bu kısım pakete ham veri ekler.

Bu mesajı gönderdikten sonra dinleme yaptığımız Scapy terminaline dönüp CTRL + C yapabiliriz. Aldığımız çıktı aşağıdaki gibidir;

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed3.webp' | relative_url }}" width="600" height="80" alt="Özel oluşturulan ICMP paketinin gönderimi sonrası Scapy sniff çıktısı">
</div>

Bu çıktıyı kaydedip içeriğini inceleyelim.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.nsummary()<br>a\[2\]
</div>

\*Bu tür ICMP paketleri genelde hedefin **ulaşılabilir olup olmadığını test etmek** için kullanılır.

##### Part 4 Create and Send a TCP SYN Packet

Şimdi sırada TCP SYN paketi oluşturup göndermek var. Yine ilk başta olduğu gibi interface’imizi dinlemeye alalım.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sniff(iface=”br-internal”)
</div>

Diğer Scapy terminaline geçelim ve paketi oluşturmaya başlayalım.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> send(IP(dst="10.6.6.23")/TCP(dport=445, flags="S"))
</div>

Önceki oluşturduğumuz ICMP paketimiz ile benzerlik olduğunu görebiliyoruz. Bu paketi de bölümlere ayırıp inceleyelim.

- **IP(dst="10.6.6.23")**: Bu kısım IP katmanını tanımlar. Paketin gideceği hedefi işaret eder.
- **TCP(dport=445, flags="S")**: Bu kısım TCP katmanını tanımlar. Hedef TCP portunu ve bayrağı işaret eder. Bayrak değeri S olduğu için bu bir TCP SYN yani bağlantı başlatma işlemidir.

Bu aslında kabaca bir port tarama işlemidir, nmap gibi araçlar bunu otomatikleştirirken el ile de böyle port taraması gerçekleştirebiliriz. Portun açık olup olmadığını anlamak için ise akıştaki paketleri incelemek gerekmektedir. Eğer gelen cevap paketinde flags değer “SA” yani SYN-ACK ise port açık anlamında gelmektedir.

Komutu gönderdikten sonra dinleme terminali üzerinden CTRL + C yaparak dinlemeyi durduralım. Trafiği kaydedip inceleyelim.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> a=\_<br>a.nsummary()<br>a\[2\]<br>a\[3\]
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/sniffed4.webp' | relative_url }}" width="1000" height="300" alt="TCP SYN paketi gönderimi sonrası yakalanan SYN ve SYN-ACK paketleri">
</div>

2\. paket bizim bağlantı başlatmak için gönderdiğimiz flags değeri “S” olan pakettir. 3. Paketi incelediğimizde ise flags değerinin SA yani SYN-ACK olduğunu görüyoruz. Bu demek oluyor ki 445 portu açık ve bağlantı isteğimizi onaylamış.

#### 3.2.6 Lab – Network Sniffing with Wireshark

##### Part 1 Capture and Save Network Traffic

Bu partta CLI üzerinden tcpdump kullanarak trafiği yakalayacağız. Trafiği pcap dosyası olarak kaydettikten sonra Wireshark veya benzeri bir uygulama üzerinden inceleyeceğiz.

Terminali açıp aşağıdaki komutu girelim;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ifconfig
</div> 

Burada Ethernet adaptörünün (genelde eth0) adını kopyalayın. Sonrasında tcpdump aracını kullanmak için terminale;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> sudo tcpdump -i eth0 -s 0 -w packetdump.pcap
</div> 

yazalım. Bu komutu açıklayalım;

- **-i eth0:** Hangi ara yüzü üzerinden trafiğin dinleneceğini belirtir.
- **-s 0:** Paketi tamamen al hiçbir kısmını atlama demektir.
- **-w packetdump.pcap:** Yakalanan paketleri ekrana yazdırmak yerine dosyaya kaydet.

Bu komutu yazdıktan sonra tcpdump bizi dinlemeye başlıyor. Web arayıcısına giderek trafik üretmeye başlayabiliriz. Ürettikten sonra tekrardan terminale gelip trafiği CTRL + C ile durdurabiliriz. Sonuçların kaydedildiği dosyayı Wireshark üzerinde inceleyebiliriz.

##### Part 2 View and Analyze the Packet Capture

Wireshark ara yüzünü açtıktan sonra **File>Open** sekmesinden packetdump.pcap isimli dosyayı incelemek üzere açabiliriz.

Tarayıcada bir web sitesine erişmek istediğinizde bilgisayar DNS sunucu IP adresine bir DNS sorgusu gönderir. DNS kayıtlarını yakaladığımız pcap dosyasında incelersek de kullanıcının ziyaret ettiği site alan adlarını ve IP adreslerini görebliriz.

Web trafiği oluştururken ziyaret ettiğimiz skillsforall.com sitesini Wireshark üzerinde filtreleyelim.

**Step 1: Analyze DNS traffic**

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/skillsforall.webp' | relative_url }}" width="880" height="120" alt="Wireshark'ta skillsforall.com için filtrelenmiş DNS trafiği">
</div>

Search iconuna skillsforall.com yazdıktan sonra çıkan alttaki menüden “String” değerini ve skillsforall kelimesini yazalım. Yukarıdaki ekran görüntüsünde yaptıklarımızı görebilirsiniz. İlk çıkan paketi incelemek için üzerine tıklayalım.

Burada yer alan Ethernet II kısmında hem destination hem de source MAC adreslerini görebilirsiniz. Teyit etmek için terminal üzerinden ifconfig komutunu yazıp eth0 ara yüzünün MAC adresine bakabilirsiniz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/destination.webp' | relative_url }}" width="1000" height="180" alt="Wireshark'ta Ethernet II katmanındaki kaynak ve hedef MAC adresleri">
</div>

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/eth0.webp' | relative_url }}" width="950" height="200" alt="ifconfig komutu ile görüntülenen eth0 arayüzünün MAC adresi">
</div>

Paket bilgileri kısmında Domain Name System query bölümünü inceleyim. Burada DNS server’ına ne gönderildiğinin detayını bulabilirsiniz. Ayrıca DNS server’ının cevabın Wireshark’ta hangi paket olduğunu belirten bir Response In kısmı da vardır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/response.webp' | relative_url }}" width="600" height="450" alt="Wireshark'ta DNS sorgu paketinin detay ve Response In bilgisi">
</div>

**Step 2: Analyze an HTTP session**

Kali makinemiz üzerinde hazır halde yüklü olan DVWA sayfasına erişip login olmayı deneyeceğiz. Bunu da Wireshark üzerinde görüntüleyerek kullanıcı bilgilerini elde etmeye çalışacağız. Bunun için ilk öncelikle DVWA sunucusunun IP bloğunun ara yüz adını öğrenmemiz gerekiyor. DVWA 10.6.6.13 adresinde yer almaktadır.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/br-inter.webp' | relative_url }}" width="890" height="200" alt="DVWA sunucusunun bulunduğu br-internal ağ arayüzünün tespiti">
</div>

Burada görüldüğü gibi br-internal ara yüzümüzün ismidir. Wireshark’ı açtıktan sonra aşağıda yer alan ara yüz isimlerinden br-internal ara yüzünü seçiyoruz. Böylece Wireshark br-internal ara yüzünü dinlemeye başlıyor. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/capture.webp' | relative_url }}" width="800" height="270" alt="Wireshark arayüz listesinde seçilen br-internal dinleme arayüzü">
</div>

Dinlemeye başladıktan sonra tarayıcı üzerinden 10.6.6.13 adresine yani DVWA sayfasına erişiyoruz. Giriş yapmak için **admin** ve **password** değerlerini giriyoruz. Değerleri girdikten sonra tarayıcı kapatıp Wireshark’ta yukarıdaki kırmızı kareye basarak dinlemeyi durduruyoruz. Arama menüsüne String değerini, arama yerine ise POST yazıyoruz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/postt.webp' | relative_url }}" width="1200" height="70" alt="Wireshark'ta String POST araması ile bulunan login isteği paketi">
</div>

Çıkan pakette login.php üzerinden bilgi gönderildiği görülüyor. Paketin HTML Form URL Encoded kısmında login bilgilerini görebilirsiniz. 

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/hypertext.webp' | relative_url }}" width="830" height="250" alt="HTML Form URL Encoded alanında görülen DVWA giriş bilgileri">
</div>

Cookieler birçok farklı amaç için kullanılır. En yaygın olarak, bir kullanıcının oturum bilgilerini saklamak için kullanılırlar. Çerezler ele geçirilebilir ve kullanıcının oturumu çalınabilir. İlk çerez, Set-Cookie değeri ile HTTP yanıtı içinde gönderilir.

Wireshark üzerinde 302 Found diye aratarak ilk çerezi bulabiliriz.

<div style="text-align: center;">
  <img loading="lazy" src="{{ '/assets/images/ciscomodule3_active/set.webp' | relative_url }}" width="880" height="620" alt="302 Found yanıtında Set-Cookie ile atanan PHPSESSID çerezi">
</div>

Çıktıda görüldüğü gibi PHPSESSID çerezi atanmıştır.
