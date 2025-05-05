---
categories: [modul]
layout: post
desc: "Cisco Ethical Hacker kursunun ikinci bölümüdür. Sızma testi sürecinde planlama ve kapsam belirleme aşamalarının neden kritik olduğunu vurgular. Aynı zamanda regülasyonlara uyum, yasal sorumluluklar ve etik ilkeler çerçevesinde nasıl hareket edilmesi gerektiğini detaylandırır."
logo: "/assets/images/cisco.png"
author: Buse Naz Yılmaz
title: Cisco Modül 3 - Active Recon 
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

Paket oluşturarak bilgi toplama yaparken, Scapy en çok tercih edilen toolllar arasındadır. Scapy, paket oluşturma için kullanılan Python tabanlı bir sistemdir. Scapy kullanmak için root izni gerekmektedir ve terminale direkt sudo scrapy yazıldığında kullanabilmektedir.

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
<span class="highlight">kali@kali</span> nmap –script smb-enum-users.se -p139,445 10.6.6.23
</div> 
