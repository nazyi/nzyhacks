---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun üçüncü bölümünün aktif bilgi toplama kısmıdır. aktif bilgi toplama teknikleri kapsamında Nmap tarama türleri ve numaralandırma (enumeration) yöntemleri detaylıca ele alınmıştır. Hedef sistemler hakkında daha derinlemesine bilgi edinmek amacıyla servisler, kullanıcılar, gruplar ve paylaşılan kaynaklar gibi bileşenlerin tespiti örnek araç ve komutlarla açıklanmıştır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Ethical Hacker Modül 3 - Active Recon 
order: 4
---

# Cisco Ethical Hacker

## Module 3: Information Gathering and Vulnerability Scanning

## 3.2 Performing Active Reconnaissance

Pasif bilgi toplamaktan sonra sıra aktif bilgi toplamaya geldi. İlk aşamada hedefler hakkında pasif bilgiler elde ettik örnek olarak host isimleri, çeşitli email veya subdomain isimleri vb. Sırada bu tespit edilen sistemlerin internet üzerinde herkese açık mı yoksa bir güvenli duvarı arkasında mı diye kontrol etmek geliyor. Port taraması yaparak sistem hakkında daha fazla bilgi toplamaya çalışıyoruz.

Port taramasında kullanılan en yaygın nmap aracının çıktılarını ufak bir açıklamak istedim.

![](./assets/images/Resim23.jpg)

### 3.2.1 Nmap Scan Types

Nmap üzerinde amaca göre birçok scan türü vardır. Bazıları aşağıda yer almaktadır.

**TCP Connect Scan ( -sT)**

Nmap default olarak farklı belirtilmedikçe hedef sistemle TCP bağlantısı kurmaya çalışır. Her porta TCP paketi atılarak gelen cevaba göre portun durumu belirlenir. Yani bu scan türü kapı açık mı diye bakmak için cidden kapıdan içeri girer veya kapıyı çalar. Böyle olduğu için de hedef sistemler üzerinde log tutuluyorsa loglar üstünde attacker IP bilgisi yer alabilir.

![](./assets/images/Resim24.jpg)

**UDP Scan (-sU)**

Genellikle TCP portları aranır fakat örneğin DNS, SNMP ve DHCP gibi sunucular UDP kullandıkları için amaca göre UDP portlarını da taramanız gerekebilmektedir.

![](./assets/images/Resim25.jpg)

**TCP FIN Scan (-sF)**

Bazen SYN taraması ağ filtresi veya firewall tarafından seçildiği için engellenebilir. Eğer böyle bir şey olursa farklı bir tarama yapmanız gerekebilir. TCP FIN taraması ile bunu gerçekleştirebilirsiniz. Hedef porta FIN paketi gönderilir, eğer port cidden kapalıysa RST paketi gönderir eğer port herhangi bir paket göndermezse portu açık varsayabilirsiniz. Çünkü FIN paketini görünce portun doğal hareketi ona görmezden gelmek olurdu.

\*Windows makinelerini bu tarama ile taramak doğru sonuçlar vermeyebilir. Çünkü Windows makineler portların durumuna bakmaksızın pakete cevap vermektedir.

![](./assets/images/Resim26.jpg)

**Host Discovery Scan (-sn)**

Bir ağ üzerindeki hostları keşfetmek için kullanılır. Ağa özel farklı ICMP mesajları atarak aktif olan hostları belirler.

**Zamanlama Opsiyonları**

6 çeşit zamanlama seçeneği -T parametresi ile ayarlanabilir. Aşağıda seçenekler vardır.

\-T0: Diğer adıyla paranoid, fark edilmemek için çok yavaş paket gönderir.

\-T1: Sneaky, yavaş paket gönderir.

\-T2: Polite, daha az bant genilşiği için yavaşlar.

\-T3: Default, hedefin cevabına göre dinamik olarak paket gönderir.

\-T4: Aggressive, hızlı paket gönderir.

\-T5: Insane, çok hızlı paket gönderir, açık portları da atlayabilir.

### 3.2.2 Types Of Enumeration

Bilgi toplama aşamasında gerçekleştirilmesi gereken numaralandırma tekniklerine sıra geldi. Numaralandırma dediğimiz terim hedef sistem üzerindeki aktif kaynakları ve servisleri daha ayrıntılı şekilde keşfetmektir.

Yani sadece kapı açık mı? diye değil kapının arkasında ne var, kim var? diye kontrol etmektir.

Birkaç numaralandırma başlığına bakalım.

#### Host Enumeration

Host numaralandırması bilgi toplama aşamasında yapılması gereken ilk görevlerden biridir. İki tarzda gerçekleşebilir:

·        **Dış ağda**: Sadece test kapsamındaki IP adreslerini taramaya özen gösterin.

·        **İç ağda:** Hedefin kullandığı tüm IP alt ağları taranır.

#### User Enumeration

Kullanıcı bilgilerini toplamak için birden fazla araç ve yöntem vardır. Bunlardan en basit örneği olarak 445 portunu kullanan SMB (Server Message Block), protokolünü verebiliriz.

Aşağıda SMB mesaj illüstrasyonunu inceleyelim.

![](./assets/images/Resim27.jpg)

SMB\_COM\_NEGOTIATE: Sunucuya hangi protokolleri veya bayrakları desteklediğini sorduğu mesajdır. Sunucu da desteklediği protokoller ve bayrakları söyleyerek geri mesaj atar.

SMB\_COM\_SESSION\_SETUP\_ANDX: Bu mesajda saldırgan, oturum açmak için izin ister. Ben guest kullanıcısıyım. Şifrem bu bağlanabilir miyim?

#### Group Enumeration

Bu işlem hedef ortamdaki kullanıcılarının hangi yetki rollerinin kullanıldığını anlamak için yapılır. Böylece yol haritası biraz daha belirginleşir. Yetki yükseltme denemeleri için yol gösterici olur.

Örnek nmap syntax’i;

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap --script smb-enum-groups.nse -p 445 host
</div>

nmap taramasının sonucunda gelen çıktada yer alan RID ve SID terimlerini inceleyelim.

·        **SID:** Bir gruba ya da kullanıcıya ait benzersiz kimlik numarasıdır.

·        **RID:** SID’nin sonundaki kısımdır ve kullanıcı veya grubu Windows bazında tanımlar.

![](./assets/images/Resim28.jpg)

#### Network Share Enumeration

Bir ağda dosya, klasör ve yazıcı paylaşan sistemleri tespit etmeye Network Share Enumeration denir. Bunları bulmaya yönelik örnek nmap komutu aşağıda yer almaktadır.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap --script smb-enum-shares.nse -p 445 host
</div>

#### Additional SMB Enumeration Examples

Bir sistemde çalışan uygulamaları ve işletim sistemlerini daha detaylı tanımlamak ve ek bilgi öğrenmek için;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sC  target\_ip
</div> 
  
Eğer hem daha detaylı bilgi hem de işletim sistemi tespiti de istersen;
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sC -sV -0  target\_ip
</div> 

Ve tablo ile nmap smb enum scriptleri hakkında bilgi vermek istedim.

![](./assets/images/Resim29.jpg)

SMB üzerinden bilgi çekmek için bir farklı tool olan enum4linux da vardır.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> enum4linux target\_ip
</div> 
 
Başka bir örnek smbclient toolu.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> smbclient -L target\_ip<br><span class="highlight">kali@kali</span> smbclient  //target\_ip/user
</div> 

#### Web Page Enumeration/Web Application Enumeration

Hedef host üzerinde bir web server çalıştığını belirlersek, saldırı ara yüzünü belirlemek için nmap scripti olan http-enum scriptini kullanabiliriz. Bu script sayesinde klasör veya dosya pathlerini brute-force kullanarak bulabiliriz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sV –script=http-enum -p 80 target\_ip
</div>  

Bahsedilmesi gereken bir farklı tool ise Nikto aracıdır. Nikto, açık kaynak kodlu web zafiyetlerini tarayan bir araçtır. Basit bir nikto kullanım komutuna aşağıda yer almaktadır.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nikto -h target_ip
</div>

#### Service Enumeration

Uzaktaki bir sistemde çalışan servislerin (hizmetlerin) belirlenmesi işlemidir. Aşağıdaki komut ile uzaktaki bir Windows sisteminde hangi servislerin detaylı olarak tespit etmek mümkündür.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap –script smb-enum-process.nse -p 445 –script-args smbuser=user , smbpass=pass
</div> 

#### Exploring Enumeration via Packet Crafting

Paket oluşturarak bilgi toplama yaparken, Scapy en çok tercih edilen toolllar arasındadır. Scapy, paket oluşturma için kullanılan Python tabanlı bir sistemdir. Scapy kullanmak için root izni gerekmektedir ve terminale direkt sudo scapy yazıldığında kullanabilmektedir.

Örnek, malicious\_payload ile ICMP paketi oluşturmak için aşağıdaki komutu kullanabiliriz.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> send(IP(dst=”192.168.88.251”)/ICMP()/”malicious\_payload”)
</div>

Bu paketi gönderirken aynı sırada tshark ile kendi ağımızı dinlersek ICMP paket isteğini görüntüleyebiliriz. 

![](./assets/images/Resim30.jpg)

\*tshark, Wireshark’ın terminal sürümüdür.

Scapy üzerinde kullanılabilecek birçok protokol vardır. Bu prokolleri listelemek için **ls()** fonksiyonunu kullanabilirsiniz. Mesela TCP protokolünü destekleyen formatları görmek için **ls(TCP)** komutunu kullanabilirsiniz.

explore() komutu ile Scapy ara yüzüne erişip format ve prokollere inceleyebilirsiniz.

### 3.2.3 Lab – Enumeration with Nmap

#### Part 1 Investigate Nmap

**Step 1: Investigate Nmap Options and Features**

Common NMAP ayarlarına bakalım. man nmap diyerek aşağıdaki parametreleri bulabilirsiniz.

·        \-A: OS detection

·        \-O: OS detection

·        \-p: Port scope

·        \-sF: TCP FIN scan

·        \-ss: TCP SYN scan

·        \-sT: TCP scan

·        \-sV: Açık portların servis ve versiyon bilgisini bulma

·        \-T<0-5>: Tarama hızını ayarlama

·        \-v: Çıktının ayrıntısını artırır

·        \--open: Sadece açık portları gösterir

#### Part 2 Perform Basic Nmap Scans

Senaryomuza göre DMZ alanında bir hostta şüpheli davranış varmış. İlk olarak DMZ scope aralığında aktif kaç host olduğuna bakalım.

**Step 1: Initiate a basic Nmap scan of the target computer**
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -sn 10.6.6.0/24
</div> 

Verilen çıktıda toplamda 7 tane hostun aktif olduğunu görüyoruz.

Wireshark üzerinde 10.6.6.23 hostunun şüpheli olduğu söyleniyor spesifik olarak onu inceleyelim.

![](./assets/images/Resim31.jpg)

**Step 2: Obtain additional information about the host and services**

Hostun 21 numaralı portu olan FTP servisi hakkında daha fazla bilgi alalım.

![](./assets/images/Resim32.jpg)

\-A parametresi, OS keşfi, versiyon keşfi ve script taraması gibi çoğu maddeyi kapsar. Fakat kullanırken IDS tarafından tespit edilebilirsiniz. Daha fazla bilgi edinmek için aşağıdaki komutu girelim.
<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap -p21 -sV -A 10.6.6.23
</div> 

![](./assets/images/Resim33.jpg)

Çıktıda gözüktüğü gibi anon girişi kabul edilmektedir ve birkaç tane txt dosyası yer almaktadır.

**Step3: Investigate SMB services with scripts**

Server Message Block yani SMB hem Windows hem de Linux makinelerde dosya paylaşımı desteklemektedir. 139 ve 445 numaralı portlarda çalışmaktadır. Bu portlar hakkında nmap ile daha fazla şey öğrenelim.

![](./assets/images/Resim34.jpg)

Daha önce de bahsettiğimiz gibi nmap içinde bazı scriptler sayesinde istenilen sistem hakkında daha detaylı bilgi sahibi olunabilir. Hazır SMB portlarının açık oluğunu gördüğümüze göre nmap üzerindeki SMB scriptlerini çalıştırıp daha fazla bilgi edinebiliriz.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> nmap –script smb-enum-users.nse -p139,445 10.6.6.23
</div> 

![](./assets/images/Resim35.jpg)

Çıktıda görüldüğü üzere iki tane kullanıcı adı bulabildik Arbiter ve Masterchief.

Şimdi de yine bir script kullanarak SMB üzerinde paylaşılmış dosyaları görelim.

![](./assets/images/Resim36.jpg)

Burda başında $ işareti olan 2 tane gizli paylaşım bulduk ve altta yer alan Anonymous Access: read/write olması çok kritik bir risktir.

### 3.2.4 Packet Inspection and Eavesdropping

Wireshark, tshark ve tcpdump gibi araçlarla paket yakalamaları yapılabilir, paketler incelenebilir ve dinleyebilirsiniz. Penetrasyon test uzmanları için bu tür araçlar, pasif keşif yapmak için kullanışlı olabilir. Tabii ki, bu tür bir keşif, hedefe fiziksel ya da kablosuz bir bağlantı gerektirir.

### 3.2.5 Lab – Packet Crafting with Scapy

#### Part 1 Investigate the Scapy Tool

IP paketi göndermeden önce IP paketinin içeriğini anlamak önemlidir. Her IP paketinde, paket yapısı hakkında bilgi veren başlık eşlik eder. Her binary değeri IP paketinde farklı anlamlara gelmektedir.

ls() fonksiyonu ile alanlar hakkında detayları inceleyebilirsiniz. Scapy içerisinde fonksiyon kullanmanın genel mantığı function\_name (arguments) şeklindedir. Alanlar hakkında daha fazla bilgi almak için ise ls(IP) komutunu çalıştırabilirsiniz.

Aşağıdaki tabloda alan adları ve açıklamaları verilmiştir. 

![](./assets/images/Resim37.jpg)

#### Part 2 Use Scapy to Sniff Network Traffic

Ağ trafiğini, tcpdump veya tshark gibi görüntülemek için Scapy aracını kullanabiliriz.

**Step 1: Use the sniff() function**

Default olarak eth0 ağını dinlemek için direkt olarak;

·        sniff()

Sniff ile ağımızı dinliyorken yan terminal üzerinden pingleyerek gönderilen paket sayısını görüntüleyelim.

Scapy komut terminalinde dinlemeyi açtık. Yanda başka bir terminal üzerinde ping komutumuzu gönderelim.


<div class="code-window">
<br>
<span class="highlight">kali@kali</span> ping -c 5 www.cisco.com
</div>

Scapy terminalinde Ctrl + C yaptıktan sonra gelen çıktıda gelen paketlerin sayısı yer almaktadır.

![](./assets/images/Resim38.jpg)

**Step 2: Capture and save traffic on a spesific interface**

ifconfig üzerinde 10.6.6.1 ip adresinin interface ismini bir kenara not alalım. Scapy aracının terminale gelip aşağıdaki komutu yazalım;

·        sniff(iface=”br-internal”)

Yukarıda yaptığımız gibi sniff fonksiyonu ağı dinlemeye yaramaktadır. Fakat default olarak eth0 interface’ini dinlediğinden bahsetmiştik. Bu sefer bu komutta belirli bir interface üzerinden dinleme yapıyoruz. Br-internal ise virtual makineler için köprü interface idir.

Komutu girdikten sonra bu sefer Mozilla üzerinden 10.6.6.23 adresini açıyoruz.

![](./assets/images/Resim39.jpg)

Gravemind sayfası geldikten sonra Scapy terminalinden dinlemeyi durdurabiliriz Ctrl + C yaparak çıktıyı görüntüleyebilirsiniz.

![](./assets/images/Resim40.jpg)

Trafiği görüntülemek için ilk öncelikle bir değişkene kaydedip sonrasında görüntüleyebiliriz.

·        a=\_

·        a.summary()

**Step 3: Examine the collected packets**

Scapy üzerinden yine br-internal isimli interface’imizi dinlemeye alalım. Fakat bu sefer sadece ICMP protokolünün paketlerini ve toplamda 10 paket yakalamasını isteyelim.

·        sniff(iface=”br-internal”,filter=”ICMP”,count=10)
Farklı bir sekmeye giderek 10.6.6.23 IP adresine ping atalım.

·        ping -c 10 10.6.6.23

Scapy terminaline gelerek kaç tane ICMP paketinin yakalandığını görebilirsiniz. Örnek yukarıdaki çıktıda verilmiştir. Yakalanan paketleri kaydedip görüntülemek için;

·        a=\_

·        a.nsummary()
\*nsummary() ve summary() benzer fakat farklı komutlardır. nsummary() komutu birden fazla paketi görüntülemeye yararken summary() komutu yalnızca tek paketi görüntülemeye yarar.

Eğer paket hakkında daha fazla bilgi istersiniz paket numaralarının başındaki sıfırları almadan paketin numarasını yazarak bilgi alabilirsiniz. Aşağıda örneği verilmiştir;

·        a\[2\]

![](./assets/images/Resim41.jpg)

Bu çıktıları pcap dosyası olarak kaydedip Wireshark üzerinde de inceleyebiliriz. Bunu yapmak için aşağıdaki komutları kullanabiliriz.

<div class="code-window">
<br>
<span class="highlight">kali@kali</span> wrpcap(“capture1.pcap”, a)
</div> 

Kaydedilen pcap dosyasını Wireshark üzerinde inceleyebiliriz.

![](./assets/images/Resim42.jpg)

#### Part 3 Create and Send an ICMP Packet

ICMP, ağ cihazları arasında kontrol mesajları göndermek amacıyla tasarlanmış bir protokoldür. Birçok farklı türde ICMP paketi vardır.

**Step 1: Use interactive mode to create and send a custom ICMP packet.**

Scapy terminali üzerinde “br-internal” isimli interface’i dinlemeye başlayalım.

·        sniff(iface=”br-internal”)

Dinlemeye başladıktan sonra yeni bir terminal açıp sudo izniyle birlikte tekrardan bir Scapy terminali açalım. Burada kendi ICMP paketimizi oluşturup 10.6.6.23 IP adresine göndereceğiz.

·        send(IP(dst="10.6.6.23")/ICMP()/"This is a test")

Bu komutumuzu bölümleriyle birlikte inceleyelim.

·        **IP(dst="10.6.6.23")** : Bu kısım IP katmanını oluşturur. dst ile paketin nereye gideceğini belirtiyoruz.

·        **/ICMP()** : IP katmanının üstüne ICMP katmanı eklenir. Default olarak echo-request mesajı oluşturulur g eğer farklı bir tipte ICMP mesajı oluşturmak istiyorsanız type fonksiyonunu kullanabilirsiniz örneğin type=0.

·        **/”This is a test”** : Bu kısım pakete ham veri ekler.

Bu mesajı gönderdikten sonra dinleme yaptığımız Scapy terminaline dönüp CTRL + C yapabiliriz. Aldığımız çıktı aşağıdaki gibidir;

![](./assets/images/Resim43.jpg)

Bu çıktıyı kaydedip içeriğini inceleyelim.

·        a=\_

·        a.nsummary()

·        a\[2\]
\*Bu tür ICMP paketleri genelde hedefin **ulaşılabilir olup olmadığını test etmek** için kullanılır.

#### Part 4 Create and Send a TCP SYN Packet

Şimdi sırada TCP SYN paketi oluşturup göndermek var. Yine ilk başta olduğu gibi interface’imizi dinlemeye alalım.

·        sniff(iface=”br-internal”)

Diğer Scapy terminaline geçelim ve paketi oluşturmaya başlayalım.

·        send(IP(dst="10.6.6.23")/TCP(dport=445, flags="S"))

Önceki oluşturduğumuz ICMP paketimiz ile benzerlik olduğunu görebiliyoruz. Bu paketi de bölümlere ayırıp inceleyelim.

·        **IP(dst="10.6.6.23")** : Bu kısım IP katmanını tanımlar. Paketin gideceği hedefi işaret eder.

·        **TCP(dport=445, flags="S")** : Bu kısım TCP katmanını tanımlar. Hedef TCP portunu ve bayrağı işaret eder. Bayrak değeri S olduğu için bu bir TCP SYN yani bağlantı başlatma işlemidir.

Bu aslında kabaca bir port tarama işlemidir, nmap gibi araçlar bunu otomatikleştirirken el ile de böyle port taraması gerçekleştirebiliriz. Portun açık olup olmadığını anlamak için ise akıştaki paketleri incelemek gerekmektedir. Eğer gelen cevap paketinde flags değer “SA” yani SYN-ACK ise port açık anlamında gelmektedir.

Komutu gönderdikten sonra dinleme terminali üzerinden CTRL + C yaparak dinlemeyi durduralım. Trafiği kaydedip inceleyelim.

·        a=\_

·        a.nsummary()

·        a\[2\]

·        a\[3\]

![](./assets/images/Resim44.jpg)

2\. paket bizim bağlantı başlatmak için gönderdiğimiz flags değeri “S” olan pakettir. 3. Paketi incelediğimizde ise flags değerinin SA yani SYN-ACK olduğunu görüyoruz. Bu demek oluyor ki 445 portu açık ve bağlantı isteğimizi onaylamış.

### 3.2.6 Lab – Network Sniffing with Wireshark

#### Part 1 Capture and Save Network Traffic

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

·        **\-i eth0 :** Hangi  ara yüzü üzerinden trafiğin dinleneceğini belirtir.

·        **\-s 0 :** Paketi tamamen al hiçbir kısmını atlama demektir.

·        **\-w packetdump.pcap :** Yakalanan paketleri ekrana yazdırmak yerine dosyaya kaydet.

Bu komutu yazdıktan sonra tcpdump bizi dinlemeye başlıyor. Web arayıcısına giderek trafik üretmeye başlayabiliriz. Ürettikten sonra tekrardan terminale gelip trafiği CTRL + C ile durdurabiliriz. Sonuçların kaydedildiği dosyayı Wireshark üzerinde inceleyebiliriz.

#### Part 2 View and Analyze the Packet Capture

Wireshark ara yüzünü açtıktan sonra **File>Open** sekmesinden packetdump.pcap isimli dosyayı incelemek üzere açabiliriz.

Tarayıcada bir web sitesine erişmek istediğinizde bilgisayar DNS sunucu IP adresine bir DNS sorgusu gönderir. DNS kayıtlarını yakaladığımız pcap dosyasında incelersek de kullanıcının ziyaret ettiği site alan adlarını ve IP adreslerini görebliriz.

Web trafiği oluştururken ziyaret ettiğimiz skillsforall.com sitesini Wireshark üzerinde filtreleyelim.

**Step 1: Analyze DNS traffic**

![](./assets/images/Resim45.jpg)

Search iconuna skillsforall.com yazdıktan sonra çıkan alttaki menüden “String” değerini ve skillsforall kelimesini yazalım. Yukarıdaki ekran görüntüsünde yaptıklarımızı görebilirsiniz. İlk çıkan paketi incelemek için üzerine tıklayalım.

Burada yer alan Ethernet II kısmında hem destination hem de source MAC adreslerini görebilirsiniz. Teyit etmek için terminal üzerinden ifconfig komutunu yazıp eth0 ara yüzünün MAC adresine bakabilirsiniz.

![](./assets/images/Resim46.jpg)

![](./assets/images/Resim47.jpg)

Paket bilgileri kısmında Domain Name System query bölümünü inceleyim. Burada DNS server’ına ne gönderildiğinin detayını bulabilirsiniz. Ayrıca DNS server’ının cevabın Wireshark’ta hangi paket olduğunu belirten bir Response In kısmı da vardır.

![](./assets/images/Resim48.jpg)

**Step 2: Analyze an HTTP session**

Kali makinemiz üzerinde hazır halde yüklü olan DVWA sayfasına erişip login olmayı deneyeceğiz. Bunu da Wireshark üzerinde görüntüleyerek kullanıcı bilgilerini elde etmeye çalışacağız. Bunun için ilk öncelikle DVWA sunucusunun IP bloğunun ara yüz adını öğrenmemiz gerekiyor. DVWA 10.6.6.13 adresinde yer almaktadır.

![](./assets/images/Resim49.jpg)

Burada görüldüğü gibi br-internal ara yüzümüzün ismidir. Wireshark’ı açtıktan sonra aşağıda yer alan ara yüz isimlerinden br-internal ara yüzünü seçiyoruz. Böylece Wireshark br-internal ara yüzünü dinlemeye başlıyor. 

![](./assets/images/Resim50.jpg)

Dinlemeye başladıktan sonra tarayıcı üzerinden 10.6.6.13 adresine yani DVWA sayfasına erişiyoruz. Giriş yapmak için **admin** ve **password** değerlerini giriyoruz. Değerleri girdikten sonra tarayıcı kapatıp Wireshark’ta yukarıdaki kırmızı kareye basarak dinlemeyi durduruyoruz. Arama menüsüne String değerini, arama yerine ise POST yazıyoruz.

![](./assets/images/Resim51.jpg)

Çıkan pakette login.php üzerinden bilgi gönderildiği görülüyor. Paketin HTML Form URL Encoded kısmında login bilgilerini görebilirsiniz. 

![](./assets/images/Resim52.jpg)

Cookieler birçok farklı amaç için kullanılır. En yaygın olarak, bir kullanıcının oturum bilgilerini saklamak için kullanılırlar. Çerezler ele geçirilebilir ve kullanıcının oturumu çalınabilir. İlk çerez, Set-Cookie değeri ile HTTP yanıtı içinde gönderilir.

Wireshark üzerinde 302 Found diye aratarak ilk çerezi bulabiliriz.

![](./assets/images/Resim53.jpg)

Çıktıda görüldüğü gibi PHPSESSID çerezi atanmıştır.
